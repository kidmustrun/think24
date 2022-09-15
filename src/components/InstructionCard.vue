<template>
  <div class="instruction-card p-3 my-3">
    <h2 class="instruction-card__heading">Инструкция:</h2>
    <div class="instruction-card__desc">
      {{ desc }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "InstructionCard",
  props: {
    desc: String,
  },
});
</script>
