<template>
  <div class="container">
    <input
      type="text"
      class="todo-input"
      placeholder="Un élément à ajouter?"
      v-model="newTodo"
    />
    <button v-on:click="addNewTodo">Ajouter</button>
    <div class="list-group">
      <ul>
        <List
          v-for="(item, index) in itemList"
          :key="index"
          :content="item.content"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import List from "@/components/List.vue";

export default {
  name: "Todolist",
  components: {
    List,
  },
  props: {
    newTodo: String,
  },
  data() {
    return {
      itemList: [
        { content: "Wash the car" },
        { content: "Clean the house" },
        { content: "Read Javascript good practices" },
        { content: "Got to the swimming pool" },
      ],
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodo.length > 0) {
        this.itemList.push({ content: this.newTodo });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 500px;
  margin: auto;
  padding: 20px;
}

.todo-input {
  padding: 2px 8px;
  width: 100%;
  box-sizing: border-box;
}

.list-group {
  // border: solid 1px red;
  padding: 12px 0;
  ul {
    margin: 0;
    padding: 0;
  }
}
</style>