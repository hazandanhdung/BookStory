<script lang="ts" setup>
import type { EntityInstance } from '~/types'

const props = defineProps<{
  entity: EntityInstance
  placeholder?: string
}>()

const entity = useEntityCard(props.entity)
</script>

<template>
  <article class="flex gap-4 flex-row group relative m-2 h-56 group">
    <div class="group-hover:shadow transition-all transform group-hover:scale-[1.02] duration-200 h-full relative">
      <app-img
        v-if="entity.media?.available"
        class="aspect-[4/5] w-36 flex-none rounded-md object-cover h-full"
        :src="entity.media?.url"
        :color="entity.media?.color"
        :alt="entity.media?.name"
      />
      <div v-else class="h-full aspect-[4/5] w-36">
        <img v-if="placeholder" :src="placeholder" :alt="entity.title" class="object-cover h-full rounded-md">
        <div v-else class="w-36 flex-none rounded-md object-cover h-full bg-yellow-100 text-black text-right">
          <div class="p-4 text-sm">
            <div class="text-xs">
              {{ entity.subtitle }}
            </div>
            <div class="mt-6 font-semibold">
              {{ entity.title }}
            </div>
            <hr class="border-black mt-3">
          </div>
        </div>
      </div>
      <div v-if="entity.type" class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black/80 z-10" />
      <div v-if="entity.type" class="absolute bottom-3 left-3 z-20 text-lg">
        {{ entity.type }}
      </div>
    </div>
    <div class="flex-auto relative">
      <p v-if="entity.subtitle" class="mt-1 text-sm text-gray-600 dark:text-gray-400 line-clamp-2">
        {{ entity.subtitle }}
      </p>
      <h3
        class="text-base mt-1 font-semibold text-gray-900 line-clamp-3 hyphens-auto dark:text-gray-100 group-hover:underline"
        lang="en"
      >
        {{ entity.title }}
      </h3>
      <div class="absolute left-0 bottom-2 text-sm italic text-gray-600 dark:text-gray-400">
        <div v-if="entity.text">
          <!-- <div v-if="entity.entityName" class="capitalize">
            {{ entity.entityName }}
          </div>
          <div v-if="entity.serie">
            <div>{{ entity.serie?.title }}</div>
            <div class="text-xs mt-2">
              Vol. {{ entity.serie?.volume }}
            </div>
          </div>
          {{ entity.count }} -->
          {{ entity.text }}
        </div>
        <div v-if="entity.details" class="mt-5">
          {{ entity.details }}
        </div>
      </div>
    </div>
    <typed-link
      :to="entity.route ? entity.route : { name: 'index' }"
      :title="entity.title"
      class="absolute inset-0 z-10"
    />
  </article>
</template>
