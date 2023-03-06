<template>
    <div>
        <form class="todo-form-add" @submit.prevent="addTodo">
            <input type="text" class="todo-form-add-input" placeholder="Todos..." v-model="title">
            <button class="todo-form-add-btn">Add Todo</button>
        </form>
    </div>
</template>

<script>
import { ref } from "vue";
export default {
    name: "AddTodo",
    setup(props, { emit }) {
        const title = ref('')
        function addTodo() {
            if (title.value.trim) {
                const newTodo = {
                    id: Math.floor(Math.random() * 100), 
                    title: title.value, 
                    completed: false
                }
                emit('add-todo', newTodo);
                title.value = '';
            }
        }
        return {
            addTodo,
            title
        }
    }
}
</script>

<style scoped>
.todo-form-add {
    margin-top: 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.todo-form-add-input {
    width: 100%;
    margin-right: 20px;
    height: 30px;
    padding: 10px;
    outline: none;
    border: 1px solid blue;
}

.todo-form-add-btn {
    border: 1px solid blue;
    width: 150px;
    padding: 0 10px;
    height: 30px;
    cursor: pointer;
}
</style>