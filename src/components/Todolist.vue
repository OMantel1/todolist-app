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

    <div class="color-box">
      <input
        checked="checked"
        type="radio"
        name="color"
        id="input-white"
        value="bg-white"
        class="btn-white color"
        v-model="colorPicked"
      />
      <input
        type="radio"
        name="color"
        id="input-blue"
        value="bg-blue"
        class="btn-blue color"
        v-model="colorPicked"
      />
      <input
        type="radio"
        name="color"
        id="input-orange"
        value="bg-orange"
        class="btn-orange color"
        v-model="colorPicked"
      />
      <input
        type="radio"
        name="color"
        id="input-red"
        value="bg-red"
        class="btn-red color"
        v-model="colorPicked"
      />
    </div>

    <div class="list-group" id="list">
      <p v-if="itemList.length <= 0" class="msg">Votre liste est vide</p>
      <ul v-else>
        <TodolistItems
          v-for="todo in itemList"
          :key="todo.id"
          :content="todo.content"
          :class="todo.color"
          :id="todo.id"
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
      id: "",
      itemList: [],
      newTodo: "",
      colorPicked: "bg-white",
    };
  },
  mounted() {
    this.check();
  },
  methods: {
    deleteTodoClicked(idClicked) {
      for (let i = 0; i < this.itemList.length; i++) {
        if (this.itemList[i].id === idClicked) {
          this.itemList.splice(i, 1);
          localStorage.setItem("todoStorage", JSON.stringify(this.itemList));
        }
      }
    },
    check() {
      let storage = JSON.parse(localStorage.getItem("todoStorage"));
      if (storage) {
        this.itemList = JSON.parse(localStorage.getItem("todoStorage"));
      }
    },
    addNewTodo() {
      if (this.newTodo.length > 0) {
        let id = Date.now();
        let newTodo = new todo(id, this.newTodo, this.colorPicked);
        this.itemList.unshift(newTodo);
      }
      this.newTodo = "";
      localStorage.setItem("todoStorage", JSON.stringify(this.itemList));
    },
    deleteAllTheList() {
      let group = document.getElementById("list");
      group.classList.add("fade");
      setTimeout(() => {
        this.deleteAllStorage();
        group.classList.remove("fade");
      }, 400);
    },
    deleteAllStorage() {
      localStorage.removeItem("todoStorage");
      this.itemList = [];
    },
  },
};

class todo {
  constructor(id, todo, color) {
    this.id = id;
    this.content = todo;
    this.color = color;
  }
}
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
  padding: 4px 24px;
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

.color-box {
  padding-top: 18px;
  input[type="radio"] {
    width: 22px;
    height: 22px;
    -moz-appearance: none;
  }
  input:after {
    position: relative;
    content: "";
    width: 20px;
    height: 20px;
    background-color: white;
    border: solid white 1px;
    border-radius: 50%;
    display: inline-block;
  }
  input:checked:after {
    border: solid black 1px;
  }
  .btn-blue:after {
    background-color: #74b9ff;
    border: solid #74b9ff 1px;
  }
  .btn-white:after {
    background-color: white;
    border: solid #bababa 1px;
  }
  .btn-red:after {
    background-color: #ff7675;
    border: solid #ff7675 1px;
  }
  .btn-orange:after {
    background-color: #fdcb6e;
    border: solid #fdcb6e 1px;
  }
}

.color {
  &:hover {
    animation: ball 300ms;
  }
}

.fade {
  animation: fade 0.5s;
}

@keyframes fade {
  from {
    opacity: 1;
    transform: scale(1);
  }
  to {
    opacity: 0;
    transform: scale(0.5);
  }
}

@keyframes ball {
  from {
    transform: translateX(0px);
  }
  25% {
    transform: translateX(-2px);
  }
  50% {
    transform: translateX(0px);
  }
  75% {
    transform: translateX(2px);
  }
  to {
    transform: translateX(0);
  }
}
</style>