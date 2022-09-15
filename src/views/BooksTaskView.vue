<template>
  <div class="page_green">
    <NavigationBack />
    <div class="container container_white container_padding-fix">
      <TitleOfTask title="В мире книг" />

      <div class="row">
        <div class="col-lg-6 col-12 droppable">
          <p class="invisible">hidden</p>
          <BookCard
            v-for="book in books.filter((book) => book.activated == false)"
            class="m-3"
            :key="book.id"
            draggable="true"
            @dragstart="onDragStart($event, book)"
            :img="book.img"
          />
        </div>

        <div
          v-for="category in categories"
          :key="category.categoryId"
          class="col-lg-3 col-6"
        >
          <p class="title_bold text-center" v-if="category.categoryId === 0">
            Жанры фольклора
          </p>
          <p class="title_bold text-center" v-if="category.categoryId === 1">
            Не являются жанрами фольклора
          </p>
          <div
            class="empty-card m-3"
            v-for="index in 6"
            :key="index"
            @drop="onDrop($event, category.categoryId)"
            @dragover.prevent
            @dragenter.prevent
          >
            <BookCard
              v-if="getBook(category, index)"
              draggable="true"
              :class="{
                'book-card_wrong':
                  checked &&
                  getBook(category, index).answer !=
                    getBook(category, index).categoryId,
                'book-card_right':
                  checked &&
                  getBook(category, index).answer ===
                    getBook(category, index).categoryId,
              }"
              @dragstart="onDragStart($event, getBook(category, index))"
              :img="getBook(category, index).img"
              :resultimg="[
                getBook(category, index).answer ===
                getBook(category, index).categoryId
                  ? 'success'
                  : 'error',
              ]"
              :checked="checked"
            />
          </div>
        </div>
      </div>
      <ButtonGreen class="ms-5" text="Проверить" @click="checkAnswers" />
    </div>
    <FooterCat />
  </div>
</template>
<script lang="ts">
import NavigationBack from "@/components/NavigationBack.vue";
import TitleOfTask from "@/components/TitleOfTask.vue";
import BookCard from "@/components/BookCard.vue";
import ButtonGreen from "@/components/ButtonGreen.vue";
import FooterCat from "@/components/FooterCat.vue";
import { BookType } from "@/types/book.interface";
import { CategoryType } from "@/types/category.interface";
import { ref } from "vue";

export default {
  name: "BooksTaskView",
  components: {
    NavigationBack,
    TitleOfTask,
    BookCard,
    ButtonGreen,
    FooterCat,
  },
  setup() {
    const books = ref([
      {
        id: 0,
        categoryId: 0,
        img: "book1",
        answer: 1,
        activated: false,
        sequence: 0,
      },
      {
        id: 1,
        categoryId: 0,
        img: "book2",
        answer: 1,
        activated: false,
        sequence: 0,
      },
      {
        id: 2,
        categoryId: 1,
        img: "book3",
        answer: 0,
        activated: false,
        sequence: 0,
      },
      {
        id: 3,
        categoryId: 0,
        img: "book4",
        answer: 1,
        activated: false,
        sequence: 0,
      },
      {
        id: 4,
        categoryId: 1,
        img: "book5",
        answer: 0,
        activated: false,
        sequence: 0,
      },
      {
        id: 5,
        categoryId: 1,
        img: "book6",
        answer: 0,
        activated: false,
        sequence: 0,
      },
    ]);
    const categories = ref([
      {
        categoryId: 0,
        folklore: true,
      },
      {
        categoryId: 1,
        folklore: false,
      },
    ]);
    let checked = ref(false);
    function getBook(category: CategoryType, index: number) {
      return books.value.find((book) => {
        return (
          book.answer == category.categoryId &&
          book.activated == true &&
          book.sequence == index - 1
        );
      });
    }

    function onDragStart(e: DragEvent, book: BookType) {
      checked.value = false;
      e.dataTransfer!.dropEffect = "move";
      e.dataTransfer!.effectAllowed = "move";
      e.dataTransfer!.setData("bookCategoryId", book.categoryId.toString());
      e.dataTransfer!.setData("bookId", book.id.toString());
    }
    function onDrop(e: DragEvent, categoryId: number) {
      const bookCategoryId = parseInt(
        e.dataTransfer!.getData("bookCategoryId")
      );
      const bookId = parseInt(e.dataTransfer!.getData("bookId"));

      books.value = books.value.map((book) => {
        if (book.id == bookId) {
          book.activated = true;
          book.answer = categoryId;
          let len = books.value.filter((book) => {
            return book.activated == true && book.answer == categoryId;
          }).length;
          book.sequence = len - 1;
        }
        return book;
      });
    }

    function checkAnswers() {
      checked.value = true;
      window.scrollTo(0, 0);
    }
    return {
      books,
      categories,
      onDragStart,
      onDrop,
      getBook,
      checked,
      checkAnswers,
    };
  },
};
</script>
