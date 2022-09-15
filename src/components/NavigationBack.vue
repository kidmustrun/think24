<template>
  <nav class="nav fixed-top container">
    <router-link to="/"><img src="@/assets/back.svg" />Назад</router-link>
  </nav>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "NavigationBack",
});
</script>
