<script setup>
import TodoInput from '../components/UI/TodoInput.vue';
import TodoItem from '../components/UI/TodoItem.vue';
import { Icon } from '@iconify/vue';
import { uid } from 'uid';
import { computed, ref, watch } from 'vue';

/* data */

const todoList = ref([]);
/* Watch */

watch(
    todoList,
    () => {
        setLocalStorage();
    },
    { deep: true }
);

/* computed */

const allCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted);
});

/* methods */

const createTodoHandle = (inputValue) => {
    todoList.value.push({
        id: uid(),
        inputValue,
        isCompleted: false,
        isEditing: false,
    });
};

const fetchTodoList = () => {
    const savedTodos = JSON.parse(localStorage.getItem('MyTodoList'));
    if (savedTodos) {
        todoList.value = savedTodos;
    }
};
fetchTodoList();

const setLocalStorage = () => {
    localStorage.setItem('MyTodoList', JSON.stringify(todoList.value));
};

const toggleCompleteHandle = (index) => {
    todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
    setLocalStorage();
};
const editTodoHandle = (index) => {
    todoList.value[index].isEditing = !todoList.value[index].isEditing;
};
const deleteTodoHandle = (id) => {
    todoList.value = todoList.value.filter((todo) => {
        return todo.id !== id;
    });
};
const updateTodoHandle = (targetVal, index) => {
    todoList.value[index].inputValue = targetVal;
};
</script>
<template>
    <div class="home_view">
        <header>Create Todo</header>
        <main>
            <todo-input @create-todo="createTodoHandle"></todo-input>
            <ul v-if="todoList.length > 0">
                <todo-item
                    v-for="(item, index) in todoList"
                    :todoData="item"
                    :index="index"
                    :key="item.id"
                    @toggle-complete="toggleCompleteHandle"
                    @edit-todo="editTodoHandle"
                    @delete-todo="deleteTodoHandle"
                    @update-todo="updateTodoHandle"
                ></todo-item>
            </ul>
            <div v-if="allCompleted && todoList.length > 0" class="completed_message_container">
                <Icon icon="noto-v1:party-popper" width="16" />
                <p class="completed_message">You have completed all your todos!</p>
            </div>
        </main>
    </div>
</template>

<style lang="scss" scoped>
.home_view {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: calc(100vh - 95px);
    background-color: #bfdbf7;
    color: #22577a;
    padding-bottom: 2rem;

    header {
        font-size: 32px;
        font-weight: bold;
        text-align: center;
        padding-top: 2rem;
        margin-bottom: 1rem;
    }
    main .completed_message_container {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 1rem;
        .completed_message {
            margin-left: 8px;
        }
    }
}
</style>
