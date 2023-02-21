<template>
  <div class="note__item">
    <div class="note__top">
      <h4 class="note__title">{{ note.title }}</h4>
      <p class="note__date">{{ note.date }}</p>
    </div>
    <p class="note__desc">
      {{ note.desc }}
    </p>
    <div class="note__btns" v-show="!search">
      <button class="note__btn redact" @click="$emit('changeNote', note.id)">
        <img src="@/assets/img/pen.svg" alt="" />
        <span>РЕДАКТИРОВАТЬ</span>
      </button>
      <button class="note__btn delete" @click="$emit('delNote', note.id)">
        <img src="@/assets/img/trash.svg" alt="" />
        <span>Удалить</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoteItem",
  inject: ["words"],
  props: {
    lang: String,
    search: String,
    note: {
      typeof: Object,
      default: {
        title: "",
        desc: "",
        date: "",
        id: "",
      },
    },
  },
  data() {
    return {};
  },
};
</script>

<style>
</style>