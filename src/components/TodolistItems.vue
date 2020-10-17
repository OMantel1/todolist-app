<template>
  <li>
    <p>
      {{ content }}
    </p>
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
      let dataToDelete = this.content;
      this.$emit("delete-item", dataToDelete);
    },
  },
};
</script>

<style lang="scss" scoped>
li {
  list-style-type: none;
  border: solid rgb(185, 185, 213) 1px;
  text-align: left;
  padding: 0 8px;
  border-radius: 2px;
  display: flex;
  justify-content: space-between;
  p {
    margin: 2px;
  }
}

.far {
  color: #e74c3c;
}

.delete-icon {
  position: relative;
  top: 2px;
}
</style>