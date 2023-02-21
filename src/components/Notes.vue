<template>
  <div class="changer">
    <div class="container changer__wrap">
      <h3 class="all__notes">
        <div v-if="!search">
          {{ notes.length > 0 ? words.infobar[lang] : words.noinfobar[lang] }}
        </div>
        <div v-else>{{ words.appbarseacrch[lang] }}</div>
      </h3>
      <button class="ch__btn" @click="change = !change">
        <div v-if="change" class="ch__cont">
          <img src="@/assets/img/flex.svg" alt="" />
          <span> {{ words.list[lang] }}</span>
        </div>
        <div v-else class="ch__cont">
          <img src="@/assets/img/grid.svg" alt="" />
          <span>{{ words.grid[lang] }}</span>
        </div>
      </button>
    </div>
    <div class="container">
      <div :class="[change ? grid : flex]">
        <Note
          :lang="lang"
          :note="note"
          v-for="(note, index) in notes"
          :key="index"
          @changeNote="$emit('changeNote', note.id)"
          @delNote="$emit('delNote', note.id)"
          :search="search"
        />
      </div>
    </div>
  </div>
</template>
<script>
import Note from "@/components/Noteitem.vue";
export default {
  name: "NotesTodo",
  components: {
    Note,
  },
  inject: ["words"],

  props: {
    notes: {
      typeof: Array,
    },
    lang: String,
    search: String,
  },
  data() {
    return {
      change: true,
      flex: "changer__flex",
      grid: "changer__grid",
    };
  },
};
</script>

<style>
</style>