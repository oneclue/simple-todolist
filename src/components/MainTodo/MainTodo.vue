<template>
  <div class="main-todo">
    <input
      id="inp"
      v-model="contents"
      @keyup.enter="add"
      type="text"
      placeholder="What to do ?"
      autofocus
    />
    <TodoItem v-for="(item,index) in filterData" :key="index" :todo="item" @del="delClickHandler" />
    <TodoInfo
      v-if="todoData.length !== 0"
      :total="total"
      @toggleState="handleToggleState"
      @clearCom="handleClear"
    />
  </div>
</template>

<script>
import TodoItem from "./coms/TodoItem.vue";
import TodoInfo from "./coms/TodoInfo.vue";
let id = 0;
export default {
  name: "MainTodo",
  data() {
    return {
      contents: "",
      todoData: [],
      total: 0,
      filter: "全部"
    };
  },
  methods: {
    // 添加一项任务
    add() {
      if (this.contents === "") return;
      this.todoData.unshift({
        id: id,
        content: this.contents,
        completed: false
      });
      this.contents = "";
      id++;
    },
    delClickHandler(id) {
      this.todoData.splice(
        this.todoData.findIndex(item => item.id === id),
        1
      );
    },
    handleToggleState(state) {
      this.filter = state;
    },
    handleClear() {
      this.todoData = this.todoData.filter(item => item.completed === false);
    }
  },
  watch: {
    todoData: {
      deep: true,
      handler() {
        this.total = this.todoData.length;
      }
    }
  },
  computed: {
    filterData() {
      if (this.filter === "全部") {
        return this.todoData;
      }
      if (this.filter === "待办") {
        return this.todoData.filter(item => item.completed === false);
      }
      if (this.filter === "已办") {
        return this.todoData.filter(item => item.completed === true);
      }
      return [];
    }
  },
  components: {
    TodoItem,
    TodoInfo
  }
};
</script>

<style>
.main-todo {
  margin: 0 auto;
  width: 350px;
  background-color: #fff;
  box-shadow: 0 0 5px #666;
}
.main-todo > input {
  padding: 6px 6px 6px 16px;
  width: 100%;
  font-size: 24px;
  font-weight: inherit;
  font-family: inherit;
  color: inherit;
  border: none;
  outline: none;
  box-sizing: border-box;
}
/* WebKit browsers  */
input::-webkit-input-placeholder {
  color: #eeeeee;
}
/* IE10使用伪类 */
input:-ms-input-placeholder {
  color: #eeeeee;
}
</style>