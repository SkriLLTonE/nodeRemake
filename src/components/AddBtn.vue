<template>
  <button class="add__btn" @click="openModal">
    <img src="@/assets/img/pen.svg" alt="" />
  </button>
</template>

<script>
export default {
  name: "AddBtnTodo",
  methods: {
    openModal() {
      this.$emit("openModal", true);
    },
  },
};
</script>

<style>
</style>