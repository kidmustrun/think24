<template>
  <div class="container container_home">
    <h1 class="container__heading">В мире книг</h1>
    <InstructionCard
      desc="Распредели книги, ориентируясь на названия, по соответствующим рубрикам таблицы: «Жанры фольклора», «Не являются жанрами фольклора»."
    />
    <ButtonGreen @click="$router.push('task')" text="Продолжить" />
  </div>
</template>

<script>
import InstructionCard from "@/components/InstructionCard.vue";
import ButtonGreen from "@/components/ButtonGreen.vue";
export default {
  name: "HomeView",
  components: {
    InstructionCard,
    ButtonGreen,
  },
};
</script>
