<template>
<li>{{content}}</li>
</template>

<script>
export default {
  name: "List",
  props: {
      content: String
  }
};

</script>

<style lang="scss" scoped>
li {
  list-style-type: none;
  border: solid rgb(185, 185, 213) 1px;
  text-align: left;
  padding-left: 10px;
  margin: 8px 0;
  border-radius: 2px;
}

li:nth-child(even) {
  background-color: rgb(240, 240, 240);
}
</style>