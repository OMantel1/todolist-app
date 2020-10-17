<template>
  <div class="container">
    <form class="form">
      <input
        type="text"
        class="todo-input"
        placeholder="Un élément à ajouter?"
        v-model="newTodo"
        v-on:keyup.enter="addNewTodo"
      />
      <button class="addButton btn" v-on:click="addNewTodo">Ajouter</button>
    </form>

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
        this.itemList.unshift(this.newTodo);
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
  max-width: 800px;
  margin: auto;
  padding: 20px 0;
}

.form {
  display: flex;
}

.msg {
  font-size: 16px;
}

.container,
.msg {
  text-align: center;
}

.btn {
  font-family: inherit;
  padding: 0 24px;
  line-height: 22px;
  border-radius: 4px;
  border: solid #3662f3 1px;
  color: white;
  background-color: #3662f3;
  font-weight: bold;
  font-size: 14px;
  &:hover {
    box-shadow: 0px 0px 4px grey;
    cursor: pointer;
  }
}

.todo-input {
  padding: 2px 8px;
  margin-right: 4px;
  width: 100%;
  box-sizing: border-box;
  font-size: 14px;
}

.list-group {
  padding: 24px 0;
  ul {
    padding: 0;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
    @media (max-width: 425px) {
      grid-template-columns: repeat(2, 1fr);
    }
  }
}
</style>