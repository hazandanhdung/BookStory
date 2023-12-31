<script setup lang="ts">
import AppButton from '@/components/app/button.vue'
import AppLoading from '@/components/app/loading.vue'

const props = defineProps<{
  meta: ApiMeta
  endpoint: ApiTypedRouteList
}>()

const emit = defineEmits<{
  (e: 'load', payload?: ApiResponse<Entity[]>): void
}>()

const { setQuery, requestRaw } = useHttp()

const pending = ref(false)
const disabled = ref(false)

async function load() {
  pending.value = true
  const currentPage = props.meta.current_page
  const lastPage = props.meta.last_page
  const nextPage = (
    lastPage !== currentPage ? currentPage + 1 : lastPage
  ).toString()

  let endpoint = props.meta.path
  endpoint = setQuery(endpoint, {
    page: parseInt(nextPage),
    size: parseInt(props.meta.per_page),
  })

  const list = await requestRaw<ApiResponse<Entity[]>>({
    endpoint,
  })
  pending.value = false

  emit('load', list)
}
</script>

<template>
  <div>
    <div v-if="meta.current_page !== meta.last_page" class="flex">
      <transition name="fade">
        <AppButton
          v-if="!disabled"
          color="primary"
          class="w-full max-w-lg mx-auto"
          :disabled="disabled"
          align="center"
          @click="load"
        >
          <div class="flex items-center space-x-2 relative">
            <div class="absolute top-1/2 -translate-y-1/2 transform -left-5">
              <transition name="fade">
                <AppLoading v-if="pending" class="w-5 h-5" />
                <span v-else class="w-5 h-5" />
              </transition>
            </div>
            <span v-if="!disabled">Load more</span>
            <span v-else>End</span>
          </div>
        </AppButton>
      </transition>
    </div>
  </div>
</template>
