<template>
  <div class="shadow">
    <form v-on:submit.prevent="getTodo">
      <input type="text" v-model="newText" placeholder="할일을 입력" />
      <button type="submit"></button>
      <i class="fa-solid fa-plus"></i>
    </form>
  </div>
</template>

<script>
export default {
  name: "TodoInput",
  data() {
    return {
      newText: "",
    };
  },
  methods: {
    getTodo() {
      if (this.newText) {
        let value = this.newText;
        // console.log(value);
        this.$emit("addTodo", value);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
form {
  display: flex;
  height: 43px;
  input {
    flex: 1 1 0;
    padding-left: 1em;
  }
  button {
    width: 56px;
    font-size: 20px;
  }
}
</style>
