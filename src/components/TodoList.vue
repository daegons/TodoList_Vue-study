<template>
  <div id="list">
    <ul>
      <li v-for="(item, num) in todos" v-bind:key="item.id">
        <i
          v-bind:class="{
            'fa-solid': true,
            'fa-pen-to-square': !item.modify,
            'fa-floppy-disk': item.modify,
          }"
          @click="onToggle(todos, item.id)"
        ></i>
        <input
          type="text"
          @input="onInput"
          v-bind:value="item.text"
          v-bind:disabled="item.modify"
        />
        {{ item.id }}
        <i class="fa-solid fa-trash-can" @click="onRemove(todos, num)"></i>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: ["todos"],
  data() {
    return {
      inputText: "",
    };
  },
  methods: {
    onToggle(todos, id) {
      todos.map((item) => {
        if (item.id === id) {
          item.modify = !item.modify;
          if (item.modify) {
            if (this.inputText) {
              item.text = this.inputText;
            } else {
              return false;
            }
          }
        }
      });
      localStorage.todos = JSON.stringify(todos);
    },
    onInput(e) {
      console.log(e.target.value);
      this.inputText = e.target.value;
    },
    onRemove(todos, num) {
      todos.splice(num, 1);
      localStorage.todos = JSON.stringify(todos);
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
        margin: 0 10px;
        padding: 10px 5px;
        background: none;
      }
    }
  }
}
</style>
