<script setup lang="ts">
import packageJson from '~/package.json'
import LayoutFooterBackToTop from '@/components/layout/footer/back-to-top.vue'
import LayoutFooterCreativeCommons from '@/components/layout/footer/creative-commons.vue'

const appConfig = useAppConfig()

const metaAuthor = appConfig.metaAuthor
const linkLicense = appConfig.linkLicense
const linkChangelog = appConfig.linkChangelog

function date(begin: number) {
  const current = new Date().getFullYear()
  const year = `${begin} - ${current}`
  if (begin === current)
    return begin

  return year
}
</script>

<template>
  <div
    class="footer-bottom relative mt-12 items-center justify-between border-t border-gray-200 pt-8 dark:border-gray-600 lg:flex"
  >
    <div
      class="space-y-2 text-base md:flex md:items-center md:space-y-0 xl:text-center"
    >
      <div class="flex">
        <a
          href="https://creativecommons.org"
          target="_blank"
          rel="noopener noreferrer"
          title="Creative commons"
          aria-label="Creative commons"
          class="mx-auto flex items-center space-x-2 transition-colors duration-100"
        >
          <LayoutFooterCreativeCommons />
          <span>{{ date(2020) }}</span>
        </a>
      </div>
      <span class="flex">
        <span class="mx-auto md:flex">
          <span class="mx-1 hidden md:block">·</span>
          <!-- <typed-link
            v-if="team"
            :to="{
              name: 'slug',
              params: {
                slug: 'about'
              }
            }"
            class="transition-colors duration-100"
            >{{ team }}</typed-link
          > -->
          <span class="mx-auto">{{ metaAuthor }}</span>
          <span class="mx-1 hidden md:block text-center">·</span><a
            v-if="linkLicense"
            :href="linkLicense"
            target="_blank"
            rel="noopener noreferrer"
            class="block md:flex"
          >{{ packageJson.license }} license</a><span class="hidden md:block">,</span><a
            v-if="linkChangelog"
            :href="linkChangelog"
            target="_blank"
            rel="noopener noreferrer"
            class="block italic md:ml-1 md:flex text-center"
          >v{{ packageJson.version }}</a><span class="hidden md:block">.</span>
        </span>
      </span>
    </div>
    <div class="mt-6 flex lg:mt-0">
      <LayoutFooterBackToTop class="mx-auto" />
    </div>
  </div>
</template>

<style lang="css" scoped>
a {
  @apply hover:!text-gray-800 dark:hover:!text-gray-200;
}
</style>
