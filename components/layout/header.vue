<script setup lang="ts">
import type { Author } from '~/types'

interface Props {
  title?: string
  subtitle?: string
  image?: string
  imageOriginal?: string
  border?: boolean
  cta?: string
  text?: string
  type?: string
  authors?: Author[]
  // favorite?: boolean
  // entity?: Entity | Author
  color?: string
  crumbs?: string[]
}
const {
  title,
  subtitle,
  image,
  imageOriginal,
  border = false,
  cta,
  text,
  type,
  authors,
  // favorite = false,
  // entity,
  color = '#ffffff',
} = defineProps<Props>()

function getHostname(url?: string) {
  return url ? new URL(url).hostname : ''
}
</script>

<template>
  <div
    class="mb-3 border-b"
    :class="
      border
        ? 'border-gray-200 pb-6 dark:border-gray-600 md:mb-10'
        : 'border-transparent pb-2 md:mb-4'
    "
  >
    <layout-breadcrumb class="mb-6" :crumbs="crumbs" />
    <div class="lg:flex lg:items-center lg:justify-between">
      <!-- Main  -->
      <div class="flex items-center justify-between">
        <div
          :class="{ 'lg:flex lg:items-center': image }"
          class="mx-auto lg:mx-0"
        >
          <div class="flex">
            <a
              :href="image"
              target="_blank"
              rel="noopener noreferrer"
              :class="
                image
                  ? 'transition-shadow duration-100 hover:shadow'
                  : ''
              "
              class="mx-auto"
            >
              <app-img
                v-if="image"
                :src="image"
                :color="color"
                :alt="title"
                :title="title"
                class="h-20 w-20 rounded-md object-cover"
              />
            </a>
          </div>
          <div :class="{ 'mt-3 sm:ml-5 lg:mt-0': image }">
            <div class="md:flex">
              <h1
                id="message-heading"
                class="w-full text-center font-handlee text-2xl font-extrabold text-primary-600 dark:text-primary-500 lg:text-left"
              >
                {{ title }}
              </h1>
              <!-- Favoritable  -->
              <!-- <div v-if="favorite && $auth.$state.loggedIn" class="flex">
                <button
                  class="md:ml-3 p-1 mx-auto"
                  type="button"
                  aria-label="Favorite"
                  @click="toggleFavorite"
                >
                  <svg-icon
                    v-if="is_favorite"
                    name="heart-full"
                    class="w-5 h-5 text-red-600 hover:text-gray-600 transition-colors duration-100"
                  />
                  <svg-icon
                    v-else
                    class="w-5 h-5 text-gray-600 hover:text-red-600 transition-colors duration-100"
                    name="heart"
                  />
                </button>
              </div> -->
            </div>
            <!-- Authors  -->
            <div
              v-if="authors && authors.length"
              class="text-sm flex items-center mx-auto lg:mx-0 w-max lg:w-full"
            >
              <span v-if="type" class="mr-1 font-semibold">{{ type }}</span>
              <book-link-authors
                :authors="authors"
                class="text-left"
                :lowercase="type !== null"
              />
            </div>
            <h2
              class="mt-1 overflow-hidden text-ellipsis text-center text-gray-500 lg:text-left"
            >
              {{ subtitle }}
            </h2>
            <div>
              <slot name="extra" />
            </div>
          </div>
        </div>
      </div>
      <!-- Default  -->
      <div v-if="$slots.default" class="mt-6 mb-3 lg:mt-0 lg:mb-0">
        <slot />
      </div>
    </div>
    <!-- Content  -->
    <div v-if="$slots.content" class="mt-6">
      <slot name="content" />
    </div>
    <!-- About  -->
    <div
      v-if="text"
      class="word-wraping prose mt-3 max-w-full italic text-gray-500 line-clamp-3 dark:text-gray-100"
    >
      <div v-html="text" />
    </div>
    <!-- External link  -->
    <div v-if="cta" class="text-gray">
      <div class="pt-1 text-right">
        To have more informations:
        <a
          :href="cta"
          target="_blank"
          rel="noopener noreferrer"
          class="border-b border-gray-500 hover:text-gray-700"
        >{{ getHostname(cta) }}</a>
      </div>
    </div>
    <!-- Filters  -->
    <div class="mt-4">
      <slot name="filters" />
    </div>
  </div>
</template>
