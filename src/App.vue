<script setup>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
</script>

<template>
  <header>
    <img alt="Todo logo" class="logo" src="./assets/todo.png" width="60" height="60" />
    <div class="wrapper">
      <TodoHeader msg="TodoList" />
    </div>
  </header>
  <body>
    <TodoMain />
  </body>
</template>

<style scoped>
.logo {
  display: block;
  /* 文字との間のみ隙間をもうける */
  margin: 0 0.5em 0 0;
  border-radius: 5px;
}

@media (min-width: 1024px) {
  header .wrapper {
    display: flex;
    place-items: left;
    flex-wrap: wrap;
  }
}
</style>
