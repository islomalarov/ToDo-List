<template>
    <li :class="darkMode ? 'todo-item dark' : 'todo-item'" :id="todo.id">
        <input type="checkbox" class="todo-item-checkbox" @change="changeToDo(todo)">
        <div class="todo-item-info" :class="{ 'todo-item-done': todo.completed }">
            <p class="todo-item-id">{{ index + 1 }}</p>
            <p class="todo-item-title">{{ todo.title }}</p>
        </div>
        <button class="todo-item-btn" @click="$emit('todo-remove', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    name: "TodoItem",
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number,
        darkMode: Boolean
    },
    setup() {
        function changeToDo(todo) {
            todo.completed ? todo.completed = false : todo.completed = true;
        }
        return {
            changeToDo
        }
    }
}
</script>

<style scoped>
.todo-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
    color: rgb(43, 43, 101);
    border: 1px solid rgba(60, 60, 95, 0.88);
    padding: 10px;
}

.todo-item.dark {
    color: white;
    border: 1px solid rgba(228, 228, 240, 0.88);
}

.todo-item-checkbox {
    margin-right: 20px;
}

.todo-item-id {
    margin-right: 10px;
}

.todo-item-info {
    display: flex;
    align-items: center;
    flex: 1;
}

.todo-item-btn {
    width: 20px;
    height: 20px;
    border: none;
    font-size: 14px;
    cursor: pointer;
    background-color: brown;
    color: white;
}

.todo-item-done {
    text-decoration: line-through;
}
</style>