<script setup lang="ts">
import type { DownloadFile, DownloadList } from '~/types'

const props = defineProps<{
  direct?: string
  download?: DownloadFile
  files?: DownloadList
}>()

const deployable = ref(false)
const formats = ref<DownloadFile[]>()

function getOtherFormats() {
  if (props.files) {
    const list: DownloadFile[] = []
    // eslint-disable-next-line @typescript-eslint/no-unused-vars
    Object.entries(props.files).forEach(([key, value]) => {
      const file: DownloadFile = value
      if (file && file?.format !== props.download?.format)
        list.push(file)
    })
    if (list.length > 0)
      deployable.value = true

    formats.value = list
  }
}
getOtherFormats()
</script>

<template>
  <div v-if="direct">
    <app-button :href="direct" download>
      Download book
    </app-button>
    <!-- <app-button-group :action="download.url" :deployable="deployable" download title="Download">
      <div class="flex items-center justify-center w-full">
        <svg-icon name="download" class="w-5 h-5 mr-1" />
        <span class="hidden md:block mr-1">Download</span>
        <div>
          {{ download.count ? download.count : '' }}
          {{ download?.format.toUpperCase() }} ({{ download.isZip ? 'ZIP ' : ''
          }}{{ download.size }})
        </div>
      </div>
      <template #content>
        <div class="py-1" role="none">
          <span v-for="file in formats" :key="file?.format">
            <a
              v-if="file"
              :href="file.url"
              download
              class="text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-600 transition-colors duration-75 block px-4 py-2 text-sm"
              role="menuitem"
            >
              <span class="hidden md:block mr-1">Download</span>
              {{ file.count ? file.count : '' }}
              {{ file.format.toUpperCase() }} ({{ file.isZip ? 'ZIP' : '' }}
              {{ file.size }})
            </a>
          </span>
        </div>
      </template>
    </app-button-group> -->
  </div>
</template>
