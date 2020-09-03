<template>
  <form @submit.prevent="addTodo()">
    <input type="text" v-model="newTodo" placeholder="create a new TO DO" class="createTodo"/>
  </form>
</template>

<script>
export default {
  name: "CreateTodo",
  data() {
    return {
      newTodo: ""
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        this.$emit("on-new-todo", this.newTodo);
      }
      this.newTodo = "";
    }
  }
};
</script>

<style scoped lang="scss">
  .createTodo{
    font-size: 18px;
    padding: 10px 20px;
    height: 50px;
    width: 55vw;
    border: none;
    border-radius: 100px;
    outline: none;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.38);
  }
</style>
