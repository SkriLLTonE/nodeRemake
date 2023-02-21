<template>
  <transition name="show">
    <div class="modal" @click="closeModal">
      <div class="modal__content" @click.stop="">
        <form class="form">
          <h3 class="add">
            {{ edit ? "Изменить заметку" : "Добавить заметку" }}
          </h3>
          <div class="modal__inputNames">
            <p class="modal__name">Title</p>
            <input
              type="text"
              placeholder="Title"
              class="form__input"
              v-model="title"
            />
          </div>
          <div class="modal__inputNames">
            <p class="modal__name">Content</p>
            <input
              type="text"
              placeholder="Content"
              class="form__input"
              v-model="desc"
            />
          </div>
        </form>
        <div class="modal__btns">
          <div class="btn__cansel" @click="closeModal">Отмена</div>
          <div class="btn__add" v-if="!edit" @click="addNote">Добавить</div>
          <div class="btn__add" v-if="edit" @click="changeNote">Изменить</div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalTodo",
  props: {
    edit: Boolean,
    currentId: Number,
    editNote: Object,
    lang: String,
    // title:String,
    // desc:String
  },
  inject: ["words"],

  data() {
    return {
      title: "",
      desc: "",
      id: this.currentId,
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
      this.title = "";
      this.desc = "";
    },
    addNote() {
      if (this.title != "" && this.desc != "") {
        const item = {
          title: this.title,
          desc: this.desc,
          date: new Date().toLocaleDateString(),
          id: this.id++,
        };
        this.$emit("addNote", item);
        this.title = "";
        this.desc = "";
      } else {
        alert("Вы не заполнили");
      }
    },
    changeNote() {
      if (this.title != "" && this.desc != "") {
        const editedNote = {
          id: this.editNote.id,
          title: this.title,
          desc: this.desc,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("editedNote", editedNote);
        this.closeModal();
      }
    },
  },
};
</script>

<style>
</style>