<template>
  <div class="relative mt-5 mb-10">
    <div class="absolute inset-0 flex items-center" aria-hidden="true">
      <div class="w-full border-t border-gray-200 dark:border-gray-600" />
    </div>
    <div class="relative flex justify-center">
      <span class="bg-white px-2 text-gray-500 dark:bg-gray-900">
        <slot />
      </span>
    </div>
  </div>
</template>
