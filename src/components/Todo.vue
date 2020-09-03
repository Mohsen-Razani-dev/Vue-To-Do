<template>
  <li id="todo" :class="{ completed }">
    <i v-if="completed"
      class="el-icon-success"
      style="border-radius: 100%;margin-left: 20px;font-size: 24px;color: #60d8b3;box-shadow: 0 0 10px 0 rgba(51,115,96,0.41)"
    ></i>
    <i v-if="!completed"
       class="el-icon-remove"
       style="border-radius: 100%;margin-left: 20px;font-size: 24px;color: #d8c860;box-shadow: 0 0 10px 0 rgba(115,104,51,0.41)"
    ></i>
    <div
      id="todoDescr"
      @click="$emit('on-toggle')"
      v-if="!isEditing"
    >
      <span>{{ description }}</span>
    </div>
    <form v-else @submit.prevent="finishEditing()" class="editing">
      <input
        type="text"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>
    <div class="btnTodo">
      <button @click="startEditing()">
        <span>
          <i class="el-icon-edit" style="color: #5499be"></i>
        </span>
      </button>
      <button @click="$emit('on-delete')">
        <span>
          <i class="el-icon-delete" style="color: #d86060"></i>
        </span>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      isEditing: false,
      newTodoDescription: ""
    };
  },
  props: {
    description: String,
    completed: Boolean
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    }
  }
};
</script>

<style scoped lang="scss">
.completed {
  background-color: #c9ffd2 !important;
  background-size: cover;
  width: 100%;
  height: 100%;
}
#todo {
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.45);
  width: 55vw;
  background-color: white;
  margin: 20px auto;
  padding: 10px 0;
  display: flex;
  border-radius: 100px;
  align-items: center;
  cursor: pointer;
  &:hover{
    .btnTodo{
      display: flex;
    }
  }
  #todoDescr {
    height: 50px;
    width: 80%;
    display: flex;
    align-items: center;
    justify-content: left;
    font-size: 18px;
    span {
      padding-left: 20px;
    }
  }
}
.btnTodo {
  height: 100%;
  display: none;
  align-items: center;
  justify-content: center;
  button {
    outline: none;
    background-color: transparent;
    border: none;
    margin: 0 10px;
    i {
      font-size: 20px;
      cursor: pointer;
    }
  }
}
.editing {
  height: 50px;
  width: 90%;
  display: flex;
  align-items: center;
  justify-content: center;
  input {
    width: 90%;
    font-size: 17px;
    border: 1px solid #797979;
    outline: none;
    padding: 5px;
    border-radius: 10px;
  }
}
</style>
