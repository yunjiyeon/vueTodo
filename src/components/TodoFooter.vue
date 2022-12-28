<template>
  <div class="clearAllContainer shadow">
    <span @click="clearTodo" class="clearAllBtn">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
      this.$emit("removeAll");
    },
  },
};
</script>

<style scoped>
.clearAllContainer {
  background: #D7C0AE;
  border-radius: 5px;
  line-height: 50px;
  width: 150px;
  margin: 0 auto;
}
.clearAllBtn {
  color: #fff;
  cursor: pointer;
  display: block;
}
</style>