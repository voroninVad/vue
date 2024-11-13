<script setup>
import Todo from './components/Todo.vue';


</script>

<template>
  <main>
    <div class="container">
      <h1>Todo List</h1>
      <Todo />
    </div>
  </main>
</template>

<style scoped>
main{
  font-family: "Open Sans", sans-serif;
  width: 100%;
  min-height: 100vh;
  background-color: #dfebeb;
  padding-top: 50px;
}
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
  margin: 0 auto;
  width: 80%;
  background-color: #fff;
  box-shadow: #d1e1e1;
  border-radius: 30px;
}
</style>
