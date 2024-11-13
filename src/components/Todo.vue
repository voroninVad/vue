<template>
    <section class="todo__items">
        <input type="text" class="add-input" autofocus="autofocus" placeholder="Введите задачу"
            v-on:keyup.enter="addTodo" />

        <div className="filter_btn">
            <button @click="filterTodo('all')" :class="{ active: currentFilter === 'all' }">все</button>
            <button @click="filterTodo('completed')" :class="{ active: currentFilter === 'completed' }">выполненые</button>
            <button @click="filterTodo('not_completed')" :class="{active: currentFilter === 'not_completed'}">не выполненые</button>
        </div>
        <ul>
            <Item v-for="todo in renderTodos" :todo="todo" :key="todo.id" v-on:tog="toggleTodo" v-on:del="deleteTodo" />
        </ul>
    </section>
</template>

<script>
import Item from "./item.vue";

let id = 0;

export default {
    data() {
        return {
            todos: [],
            currentFilter: 'all',
        };
    },
    components: {
        Item,
    },
    computed: {
        renderTodos() {
            if (this.currentFilter === 'completed') {
                return this.todos.filter(todo => todo.status === true);
            } else if (this.currentFilter === 'not_completed') {
                return this.todos.filter(todo => todo.status === false);
            }
            return this.todos; 
        },
    },
    methods: {
        addTodo(e) {
            if (e.target.value != '') {
                this.todos.unshift({
                    id: id++,
                    content: e.target.value,
                    status: false,
                });
            }
            e.target.value = "";
        },
        deleteTodo(id) {
            this.todos.splice(
                this.todos.findIndex((todo) => id === todo.id),
                1
            );
        },
        toggleTodo(id) {
            const todo = this.todos.find(                
                (todo) => id === todo.id,
            )
            if(todo){
                todo.status = !todo.status;
            }
        },
        filterTodo(filter) {
            this.currentFilter = filter; 
        }
    },
};
</script>


<style scoped>
.todo__items {
    width: 100%;
}

.todo__form,
.filter_btn {
    width: 100%;
    display: flex;
    justify-content: space-evenly;
    margin: 20px auto;
}

ul {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 25px;
    justify-items: center;
}

@media (width <= 992px) {
  .todo__form{
    width: 100%;
    justify-content: space-between;
    gap: 10px;
    margin: 20px 0;
  }
  .filter_btn{
    width: 100%;
  }
  ul{
    grid-template-columns: 1fr 1fr;
  }
  input{
    width: 80%;
  }
  input,button{
    font-size: 18px;
    padding: 15px;
  }
}

@media (width <= 768px) {
  input{    
    width: 80%;
  }
  input,button{
    font-size: 16px;
    padding: 10px;
  }
  ul{
    grid-template-columns: 1fr;
  }
}

@media (width <= 640px){
  .todo__form{
    flex-direction: column;
    align-items: center;
    overflow: hidden;
    margin: 10px 0;
  }
  input{
    width: 100%;
  }
  .filter_btn{
    overflow-x: scroll;
    overflow-y: hidden;
    margin: 10px 0 20px;
  }
}
</style>