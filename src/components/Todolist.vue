<template>
  <div class="container">
    <input
      type="text"
      class="todo-input"
      placeholder="Un élément à ajouter?"
      v-model="newTodo"
      v-on:keyup.enter="addNewTodo"
    />
    <button class="addButton btn" v-on:click="addNewTodo">Ajouter</button>

    <!-- <p> {{dataToDelete}} </p> -->

    <div class="list-group">
      <p v-if="itemList.length <= 0" class="msg">Votre liste est vide</p>
      <ul v-else>
        <TodolistItems
          v-for="(item, index) in itemList"
          :key="index"
          :content="item"
          v-on:delete-item="deleteTodoClicked"
        />
      </ul>
    </div>

    <button
      class="clearAllButton btn"
      v-if="itemList.length > 0"
      v-on:click="deleteAllTheList"
    >
      Clear All
    </button>
  </div>
</template>



<script>
import TodolistItems from "@/components/TodolistItems.vue";

export default {
  name: "Todolist",
  components: {
    TodolistItems,
  },

  data() {
    return {
      itemList: [],
      newTodo: "",
    };
  },
  mounted() {
    this.check();
  },
  methods: {
    deleteTodoClicked(elt) {
      const indexOfElt = this.itemList.indexOf(elt);
      this.itemList.splice(indexOfElt, 1);
      localStorage.setItem("todoStorage", JSON.stringify(this.itemList));
    },
    check() {
      let storage = JSON.parse(localStorage.getItem("todoStorage"));
      if (storage) {
        this.itemList = JSON.parse(localStorage.getItem("todoStorage"));
      }
    },
    addNewTodo() {
      if (this.newTodo.length > 0) {
        this.itemList.push(this.newTodo);
      }
      this.newTodo = "";
      localStorage.setItem("todoStorage", JSON.stringify(this.itemList));
    },
    deleteAllTheList() {
      localStorage.removeItem("todoStorage");
      this.itemList = [];
    },
  },
};
</script>



<style lang="scss" scoped>
.container {
  width: 90vw;
  max-width: 500px;
  margin: auto;
  padding: 20px 0;
}

.addButton {
  margin-top: 16px;
}

.msg {
  font-size: 20px;
}

.btn {
  font-family: inherit;
  padding: 4px 24px;
  border-radius: 50px;
  border: solid #e74c3c 1px;
  color: white;
  background-color: #e74c3c;
  font-weight: bold;
  font-size: 14px;
  &:hover {
    box-shadow: 0px 0px 4px grey;
    cursor: pointer;
  }
}

.todo-input {
  padding: 2px 8px;
  width: 100%;
  box-sizing: border-box;
  font-size: 14px;
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