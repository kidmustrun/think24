<template>
  <div class="book-card p-2 position-relative text-center">
    <img
      src="@/assets/draganddrop.svg"
      class="position-absolute bottom-50 start-0 ms-2 book-card__img"
    />
    <img
      v-if="checked"
      :src="getImgUrl(resultimg)"
      class="position-absolute end-0 me-2"
    />
    <img class="book-card__img" :src="getImgUrl(img)" alt="book" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "BookCard",
  props: {
    img: String,
    resultimg: String,
    checked: Boolean,
  },
  setup(props, ctx) {
    const getImgUrl = (pic: string) => {
      return require(`../assets/${pic}.svg`);
    };
    return {
      getImgUrl,
    };
  },
});
</script>
