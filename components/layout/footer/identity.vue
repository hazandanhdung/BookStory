<script setup lang="ts">
import type { IconType } from '~~/.nuxt/svg-transformer'

const appConfig = useAppConfig()
const config = useRuntimeConfig()

const appName = appConfig.appName
const metaDescription = appConfig.metaDescription

function url(endpoint: string) {
  const apiURL = config.public.apiUrl
  return `${apiURL}${endpoint}`
}

interface Feature {
  icon: IconType
  label: string
  title: string
  link: string
}
const features: Feature[] = [
  {
    icon: 'feature-feed',
    label: 'OPDS',
    title: 'OPDS: Open Publication Distribution System',
    link: url('/opds'),
  },
  {
    icon: 'feature-catalog',
    label: 'Catalog',
    title: 'Catalog: simple interface for eReader browser',
    link: url('/catalog'),
  },
  {
    icon: 'feature-ereader',
    label: 'Webreader',
    title: 'Webreader: to read an eBook directly in your browser',
    link: url('/webreader'),
  },
  {
    icon: 'feature-api',
    label: 'API',
    title: 'API: share data between applications',
    link: url('/docs'),
  },
]
</script>

<template>
  <div class="space-y-8 xl:col-span-1">
    <div v-if="appName" class="items-center space-x-6 flex">
      <typed-link
        :to="{
          name: 'index',
        }"
        class="group flex w-max items-center lg:mx-0"
      >
        <svg-icon
          name="logo"
          class="h-6 w-6 text-gray-400 transition-colors duration-100 group-hover:text-gray dark:group-hover:text-gray-300 md:h-12 md:w-12"
        />
        <div
          class="dm:text-xl mt-2 ml-3 font-handlee text-lg text-gray-400 transition-colors duration-100 group-hover:text-gray dark:group-hover:text-gray-300 md:text-2xl"
        >
          {{ appName }}
        </div>
      </typed-link>
      <layout-option-color-mode />
    </div>
    <div class="text-base text-gray-500">
      {{ metaDescription }}
    </div>
    <div class="sm:flex sm:items-center">
      <div class="flex space-y-0">
        <a
          v-for="(feature, id) in features"
          :key="id"
          :href="feature.link"
          target="_blank"
          rel="noopener noreferrer"
          :title="feature.title"
          :aria-label="feature.title"
          class="mx-auto block w-20 rounded-md p-2 text-gray-400 transition-colors duration-75 hover:bg-gray-200 hover:text-gray dark:hover:bg-gray-800 dark:hover:text-gray-300"
        >
          <svg-icon :name="`${feature.icon}`" display="flex" class="mx-auto h-6 w-6" />
          <div class="mt-2 text-center text-xs">{{ feature.label }}</div>
        </a>
        <!-- <app-language-switch /> -->
      </div>
    </div>
  </div>
</template>
