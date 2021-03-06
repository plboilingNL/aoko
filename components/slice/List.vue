<template>
  <div class="list-block">
    <div
      v-if="slice.primary.style === 'Style1'"
      class="grid items-center grid-cols-10 gap-8 px-4 my-16 bg-gray-100 md:py-16 dark-mode:bg-gray-900 md:px-8 dark-mode:bg-black dark-mode:text-white list-slice md:my-32"
    >
      <div class="col-start-2 col-end-10 py-8">
        <h2
          class="text-3xl tracking-wider uppercase md:text-5xl"
          v-if="slice.primary.headline.length > 0"
        >{{ $prismic.asText(slice.primary.headline) }}</h2>
        <div class="w-3/12 mt-4 border-b-2 border-gray-800 dark-mode:border-gray-200 line"></div>
      </div>
      <div class="grid grid-cols-1 col-span-10 row-gap-16 md:col-span-6">
        <div class="grid grid-cols-6 col-span-1" v-for="(item, index) in slice.items" :key="index">
          <div class="col-span-2 text-4xl font-bold text-center">0{{ index + 1 }}</div>

          <div class="col-span-4 text-sm text">
            <h3 class="text-xl" v-if="item.title.length > 0">{{ $prismic.asText(item.title) }}</h3>

            <prismic-rich-text :field="item.text" v-if="item.text.length > 0" />

            <div
              class="w-3/12 mx-auto mt-8 border-b-2 border-gray-800 dark-mode:border-gray-200 line"
            ></div>
          </div>
        </div>
      </div>

      <div class="col-span-10 md:col-span-4">
        <ResponsiveImg
          v-if="slice.primary.image.url !== undefined"
          :imgobject="slice.primary.image"
          :sizes="'(min-width: 768px) 33vw, 98vw'"
        />
      </div>
    </div>

    <div
      v-else-if="slice.primary.style === 'Style2'"
      class="relative grid items-center grid-cols-10 gap-8 row-gap-16 px-4 py-16 mt-8 mt-16 mb-16 bg-gray-100 dark-mode:text-white md:px-8 dark-mode:bg-gray-900 list md:mb-32"
    >
      <div class="z-10 col-start-2 col-end-10 py-8">
        <h2
          class="text-3xl tracking-wider uppercase md:text-5xl"
          v-if="slice.primary.headline.length > 0"
        >{{ $prismic.asText(slice.primary.headline) }}</h2>
        <div class="w-3/12 mt-4 border-b-2 border-gray-800 dark-mode:border-gray-200 line"></div>
      </div>

      <template v-for="(item, index) in slice.items">
        <div
          :key="index"
          :class="`number-${index + 1}`"
          class="z-10 col-start-1 col-end-3 text-4xl font-bold text-center"
        >0{{ index + 1 }}</div>

        <div
          :key="index"
          :class="`text-${index + 1}`"
          class="z-10 col-start-3 col-end-11 text-sm text-container"
        >
          <h3 class="mb-2 text-xl" v-if="item.title.length > 0">{{ $prismic.asText(item.title) }}</h3>
          <prismic-rich-text :field="item.text" v-if="item.text.length > 0" />
          <div
            class="w-3/12 mt-8 ml-auto border-b-2 border-gray-800 dark-mode:border-gray-200 line"
          ></div>
        </div>
      </template>

      <div
        v-if="slice.primary.image.url !== undefined"
        class="absolute w-full h-full bg-white dark-mode:bg-black"
      >
        <ResponsiveImg
          :imgobject="slice.primary.image"
          :classes="'absolute w-full h-full object-cover opacity-75'"
          :sizes="'100vw'"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ResponsiveImg from '~/components/ResponsiveImg'

export default {
  components: {
    ResponsiveImg
  },
  props: {
    slice: {
      type: Object,
      default: null
    }
  }
}
</script>

<style scoped>
@screen md {
  .number-1 {
    @apply col-start-1 col-end-3;
  }
  .text-1 {
    @apply col-start-3 col-end-7;
  }
  .number-2 {
    @apply col-start-2 col-end-4;
  }
  .text-2 {
    @apply col-start-4 col-end-8;
  }
  .number-3 {
    @apply col-start-3 col-end-5;
  }
  .text-3 {
    @apply col-start-5 col-end-9;
  }
  .number-4 {
    @apply col-start-4 col-end-6;
  }
  .text-4 {
    @apply col-start-6 col-end-10;
  }
  .number-5 {
    @apply col-start-5 col-end-7;
  }
  .text-5 {
    @apply col-start-7 col-end-11;
  }
}
</style>
