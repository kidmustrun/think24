<template>
  <div class="title-card my-3 mx-1">
    <h2 class="title-card__heading text-center">{{ title }}</h2>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "TitleOfTask",
  props: {
    title: String,
  },
});
</script>
