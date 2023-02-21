<template>
  <Navbar @getSearch="search = $event" :lang="lang" @changeLang="changeLang" />
  <Notes
    :notes="filterNotes"
    @changeNote="changeNote"
    @delNote="delNote"
    :lang="lang"
    :search="search"
  />
  <AddBtn @openModal="openModal" v-show="!search" />
  <Modal
    :lang="lang"
    v-show="modalWind"
    :edit="edit"
    @closeModal="closeModal"
    :currentId="currentId"
    @addNote="addNote"
    :editNote="editNote"
    @editedNote="editedNote"
    :title="title"
    :desc="desc"
  />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import AddBtn from "@/components/AddBtn.vue";
import Modal from "@/components/Modal.vue";
import langs from "@/lang.js";
export default {
  name: "App",
  components: {
    Navbar,
    Notes,
    AddBtn,
    Modal,
  },
  data() {
    return {
      modalWind: false,
      edit: false,
      note: [],
      currentId: 1,
      editNote: {},
      langwords: {},
      search: "",
      lang: "ru",
      title: "",
      desc: "",
    };
  },
  provide() {
    return {
      words: localStorage.words ? JSON.parse(localStorage.words) : langs,
    };
  },
  computed: {
    filterNotes() {
      return this.search
        ? this.note.filter((item) =>
            item.title.toLowerCase().includes(this.search.toLowerCase())
          )
        : this.note;
    },
  },
  methods: {
    openModal() {
      this.modalWind = true;
      this.edit = false;
    },
    closeModal(status) {
      this.modalWind = status;
    },
    addNote(item) {
      this.note.push(item);
      this.modalWind = false;
    },
    getNotes() {
      const localNotes = localStorage.note;
      if (localNotes) {
        this.note = JSON.parse(localNotes);
      }
    },
    changeNote(id) {
      this.edit = this.modalWind = true;
      let pickedNote = this.note.find((note) => note.id == id);
      this.editNote = pickedNote;
      this.desc = this.editNote.desc;
      this.title = this.editNote.title;
    },
    editedNote(editedNote) {
      this.note.forEach((note) => {
        if (note.id == editedNote.id) {
          note.title = editedNote.title;
          note.desc = editedNote.desc;
          note.date = editedNote.date;
        }
      });
    },
    delNote(id) {
      let index = this.note.findIndex((note) => note.id == id);
      this.note.splice(index, 1);
    },
    changeLang(val) {
      this.lang = localStorage.lang = val;
    },
  },
  mounted() {
    this.getNotes();
    localStorage.lang = localStorage.lang || "ru";
    this.lang = localStorage.lang || "ru";
    this.langwords = langs;
    localStorage.words = JSON.stringify(this.langwords);
    console.log(localStorage);
  },
  watch: {
    note: {
      handler() {
        localStorage.note = JSON.stringify(this.note);
      },
      deep: true,
    },
  },
};
</script>

<style>
</style>
