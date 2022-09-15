<template>
  <div class="book-card p-2 position-relative">
    <img src="@/assets/draganddrop.svg" class="position-absolute bottom-50" />
    <img
      v-if="checked"
      :src="getImgUrl(resultimg)"
      class="position-absolute end-0"
    />
    <div class="book-card__img text-center">
      <img :src="getImgUrl(img)" alt="book" />
    </div>
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
