<template>
  <button class="button button_green px-4 py-2">
    {{ text }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "ButtonGreen",
  props: {
    text: String,
  },
});
</script>
