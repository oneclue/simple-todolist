<template>
  <div :class="['todo-item' , todo.completed ? 'completed' : '']">
    <input type="checkbox" v-model="todo.completed" />
    <label>{{todo.content}}</label>
    <button @click="delItem"></button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object
    }
  },
  methods: {
    delItem() {
      this.$emit("del", this.todo.id);
    }
  }
};
</script>

<style>
.todo-item {
  display: flex;
  justify-content: space-between;
  padding: 5px;
  border-top: 1px solid rgb(0, 0, 0, 0.1);
}
.todo-item:hover button::after {
  content: "x";
  color: #666;
  font-size: 18px;
  cursor: pointer;
}
.todo-item.completed label {
  color: #d9d9d9;
  text-decoration: line-through;
}
.todo-item > input {
  width: 18px;
  height: 18px;
  /* appearance: none; */
  border: none;
  border-radius: 50%;
  outline: none;
}
.todo-item > label {
  padding-left: 5px;
  line-height: 24px;
  text-align: left;
  font-size: 18px;
  flex: 1;
}
.todo-item > button {
  width: 40px;
  border: none;
  outline: none;
  background-color: #fff;
}
</style>