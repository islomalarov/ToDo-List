<template>
    <div>
        <h3 :class="darkMode ? 'todo-header dark' : 'todo-header'">Todos</h3>
        <ul class="todo-list">
            <TodoItem v-for="(todo, index) in todos" :index="index" :todo="todo" :key="todo.id" @todo-remove="removeTodo"
                :darkMode="darkMode">
            </TodoItem>
        </ul>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
    name: "TodoList",
    components: {
        TodoItem
    },
    props: {
        todos: {
            type: Array,
            required: true
        },
        darkMode: Boolean
    },
    setup(props, { emit }) {
        function removeTodo(id) {
            emit('todo-remove', id);
        }
        return {
            removeTodo
        }
    }
}
</script>

<style scoped>
.todo-header {
    color: blue;
    padding: 20px;
}

.todo-header.dark {
    color: white;
}

.todo-list {
    margin-top: 30px;
    text-align: center;
}
</style>