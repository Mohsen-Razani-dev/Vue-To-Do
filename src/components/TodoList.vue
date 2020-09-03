<template>
  <div class="TodoList">
    <div class="mainHeader">
      <el-row class="headrow">
        <el-col :md="24" class="header">
          <h1>{{ listName }}</h1>
          <i class="el-icon-s-order"></i>
        </el-col>
      </el-row>
      <el-row class="createtodo">
        <CreateTodo @on-new-todo="addTodo($event)" />
      </el-row>
      <el-divider></el-divider>
    </div>
    <div class="container">
      <el-row class="TodosRow">
        <el-col :md="24" class="todosCol">
          <ul class="todosBox">
            <Todo
              class="todos"
              v-for="(todo, index) in todos"
              :key="index"
              :description="todo.description"
              :completed="todo.completed"
              @on-toggle="toggleTodo(todo)"
              @on-delete="deleteTodo(todo)"
              @on-edit="editTodo(todo, $event)"
            />
          </ul>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import CreateTodo from "./CreateTodo";
import Todo from "./Todo";
export default {
  name: "TodoList",
  components: { Todo, CreateTodo },
  props: {
    listName: String
  },
  data() {
    return {
      todos: [
        { description: "Do the Dishes", completed: true },
        { description: "Take Out Trash", completed: false },
        { description: "Finish Doing", completed: false }
      ]
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({ description: newTodo, completed: false });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(deleteTodo) {
      this.todos = this.todos.filter(todo => todo !== deleteTodo);
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    }
  }
};
</script>

<style scoped lang="scss">
.TodoList {
  display: grid;
  align-content: center;
  justify-items: center;
  height: 100%;
  padding: 20px 0;
  .mainHeader {
    position: fixed;
    z-index: 100;
    width: 100%;
    text-align: center;
    .headrow {
      text-align: center;
      .header {
        display: flex;
        align-items: flex-end;
        justify-content: center;
        margin-bottom: 20px;
        h1 {
          font-family: Gilroy-Bold;
          font-size: 40px;
          color: #349268;
          margin: 0;
        }
        i{
          margin-left: 20px;
          font-size: 70px;
          color: #42b983;
        }
      }
    }
    .createtodo {
      width: 100%;
      text-align: center;
    }
  }
  .container {
    width: 100%;
    overflow: scroll;
    position: fixed;
    top: 26%;
    .TodosRow {
      overflow: scroll;
      min-height: 480px;
      max-height: 480px;
      .todosCol {
        .todosBox {
          padding: 20px;
        }
      }
    }
  }
}
</style>
