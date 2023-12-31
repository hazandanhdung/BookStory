<script lang="ts" setup>
import type { ApiData, Entity, Serie } from '~/types'

const { params } = useRoute()

const [serie, books] = await Promise.all([
  useHttp<Serie>({
    name: '/series/{author}/{serie}',
    params: {
      author: params.author_slug,
      serie: params.serie_slug,
    },
  }),
  useHttp<ApiData<Entity[]>>({
    name: '/series/{author}/{serie}/books',
    params: {
      author: params.author_slug,
      serie: params.serie_slug,
    },
    auto: false,
  }),
])

const crumbs: string[] = [
  'Series',
  `${serie?.author?.name}`,
  `${serie?.title}`,
]

useMetadata({
  title: `${serie?.title} by ${serie?.author?.name} · Series`,
  description: serie?.description,
  image: serie?.media_social,
})
</script>

<template>
  <main v-if="serie" class="main-content">
    <layout-header
      :title="serie.title"
      :image="serie.media?.url"
      :color="serie.media?.color"
      :subtitle="`${serie.count} books`"
      :type="serie.type"
      :authors="serie.authors"
      :cta="serie.link"
      :text="serie.description"
      :entity="serie"
      :crumbs="crumbs"
      favorite
    >
      <div class="flex">
        <book-cta-download
          :download="serie.download"
          :files="serie.files"
          class="mx-auto lg:mx-0"
        />
      </div>
      <div class="mt-2 text-center lg:text-right">
        Language: {{ serie.language.name }}
      </div>
      <template #content>
        <book-link-tags :tags="serie.tags" />
      </template>
    </layout-header>
    <section v-if="books">
      <pre>{{ books.meta }}</pre>
      <div v-if="books && books.data?.length">
        <app-divider> {{ serie.count }} Books </app-divider>
        <listing v-if="books.data?.length" :entities="books.data" type />
      <!-- <pagination-load-more
        :meta="books.meta"
        :endpoint="listRoute"
        class="mt-6 mb-5"
        @load="paginate"
      /> -->
      </div>
    </section>
  </main>
</template>
