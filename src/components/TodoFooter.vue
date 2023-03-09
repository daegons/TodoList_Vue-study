<template>
  <div id="footer">
    <span @click="allClear(todos)">전부삭제</span>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["todos"],
  methods: {
    allClear(todos) {
      localStorage.removeItem("todos");
      todos.splice(0, todos.length);
    },
  },
};
</script>

<style lang="scss" scoped>
#footer {
  text-align: center;
  span {
    display: inline-block;
    padding: 10px 20px;
    background: white;
    color: red;
    cursor: pointer;
  }
}
</style>
