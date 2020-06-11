<template>
  <div class="todo-info">
    <span>共 {{total}} 项</span>
    <div class="tabs">
      <a
        :class="[state == item ? 'actived' : '']"
        @click="toggleItem(item)"
        v-for="(item ,index) in states"
        :key="index"
      >{{ item }}</a>
    </div>
    <button @click="clearCompleted">清楚已办项</button>
  </div>
</template>

<script>
export default {
  props: {
    total: {
      type: Number
    }
  },
  data() {
    return {
      states: ["全部", "待办", "已办"],
      state: "全部"
    };
  },
  methods: {
    toggleItem(state) {
      this.state = state;
      this.$emit("toggleState", state);
    },
    clearCompleted() {
      this.$emit("clearCom");
    }
  }
};
</script>

<style>
.todo-info {
  display: flex;
  justify-content: space-between;
  padding: 5px 10px;
  border-top: 1px solid rgb(0, 0, 0, 0.1);
}
.tabs {
  display: flex;
  justify-content: space-between;
}
.todo-info > span {
  line-height: 23px;
}
.tabs > a {
  margin-right: 10px;
  border: 1px solid;
  border-radius: 6px;
  padding: 3px;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
}
.actived {
  background: #cccccc;
}
</style>