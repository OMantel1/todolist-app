<template>
  <li class="reveal">
    <p>{{ content }}</p>
    <a class="delete-icon" @click="deleteSingleItem" href="#">
      <i class="far fa-window-close"></i
    ></a>
  </li>
</template>

<script>
export default {
  name: "TodolistItems",
  props: {
    content: String,
  },
  methods: {
    deleteSingleItem() {
      let todoToDeleteID = this.$attrs.id;
      this.$emit("delete-item", todoToDeleteID);
    },
  },
};
</script>

<style lang="scss" scoped>
li {
  list-style-type: none;
  border: solid rgb(185, 185, 213) 1px;
  text-align: left;
  padding: 12px 8px;
  border-radius: 2px;
  display: flex;
  justify-content: space-between;
  p {
    margin: 2px;
  }
}

.far {
  color: #262626;
  font-size: 18px;
}

.delete-icon {
  position: relative;
  top: 2px;
}

.bg-blue {
  background-color: #74b9ff;
  border: solid #74b9ff 1px;
}
.bg-red {
  background-color: #ff7675;
  border: solid #ff7675 1px;
}
.bg-orange {
  background-color: #fdcb6e;
  border: solid #fdcb6e 1px;
}
.bg-white {
  background-color: #ffffff;
}

.reveal {
  animation: animReveal 0.7s;
}

@keyframes animReveal {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>