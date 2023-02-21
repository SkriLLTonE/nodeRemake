<template>
  <header class="header">
    <div class="header__notes">
      <button class="header__lang" @click="changeLang" v-if="lang == 'ru'">
        UZ
      </button>
      <button class="header__lang" @click="changeLang" v-else>RU</button>
      <div class="container">
        <div class="header__change">
          <transition name="opp">
            <p class="header__p" v-if="header">{{ words.appbartitle[lang] }}</p>
            <input
              type="text"
              class="header__input"
              :placeholder="words.appbarseacrch[lang]"
              v-model="search"
              v-else
            />
          </transition>
        </div>
      </div>
      <button class="header__search" @click="showSearch()">
        <div v-if="header"><img src="@/assets/img/search.svg" alt="" /></div>
        <div v-else><img src="@/assets/img/close.svg" alt="" /></div>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "NavbarTodo",
  props: {
    lang: String,
  },
  inject: ["words"],
  data() {
    return {
      search: "",
      header: true,
    };
  },
  methods: {
    changeLang() {
      this.$emit("changeLang", this.lang == "ru" ? "uz" : "ru");
    },
    showSearch() {
      this.header = !this.header;
      this.search = "";
    },
  },
  watch: {
    search(val) {
      this.$emit("getSearch", val);
    },
  },
};
</script>

<style>
</style>