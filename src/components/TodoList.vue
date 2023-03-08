<template>
  <div id="list">
    <ul>
      <li v-for="item in todos" v-bind:key="item.id">
        <i
          v-bind:class="{
            'fa-solid': true,
            'fa-pen-to-square': !item.modify,
            'fa-floppy-disk': item.modify,
          }"
          @click="onToggle(todos, item.id)"
        ></i>
        <input type="text" v-bind:value="item.text" disabled />
        <i class="fa-solid fa-trash-can"></i>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: ["todos"],
  methods: {
    onToggle(todos, id) {
      todos.map((item) => {
        if (item.id === id) {
          item.modify = !item.modify;
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
#list {
  ul {
    background: white;
    li {
      min-height: 50px;
      height: 50px;
      line-height: 50px;
      margin: 5ox 0;
      padding: 0 1em;
      display: flex;
      align-items: center;
      input {
        flex: 1;
        margin-left: 10px;
      }
    }
  }
}
</style>
