<template>
    <li>
        <span class="done" v-if="todo.status">выполнено</span>
        <span class="no-done" v-else="todo.status">не выполнено</span>
        <h4>{{ todo.content }}</h4>
        <button v-if="todo.status === false" @click="toggleTodo">выполнить</button>
        <button class="removeBtn" @click="deleteTodo">&#x2715;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
        },
    },
    methods: {
        deleteTodo() {
            this.$emit("del", this.todo.id);
        },
        toggleTodo() {
            this.$emit("tog", this.todo.id);
        }
    },
};
</script>

<style scoped>
li {
    width: 100%;
    height: 300px;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    font-size: 20px;
    border-radius: 10px;
    box-shadow: 5px 0px 5px 5px #ddd;
}

li span {
    max-width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    border-radius: 10px;
    padding: 5px;
}

li h4 {
    width: 90%;
    margin: 0 auto;
    word-break: break-all;
}

li .removeBtn {
    position: absolute;
    top: 0;
    right: 0;
    padding: 5px;
}
@media (width <= 992px) {
  li{
    font-size: 18px;
    height: 250px;
  }
}

@media (width <= 768px) {
  li{
    font-size: 16px;
    height: 250px;
  }
}
</style>