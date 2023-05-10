<script setup>
import { Icon } from '@iconify/vue';
import { ref } from 'vue';

const props = defineProps(['todoData', 'index']);
const emit = defineEmits(['delete-todo', 'toggle-complete', 'update-todo', 'edit-todo']);

const checkboxClickHandle = () => {
    emit('toggle-complete', props.index);
};

const editHandle = () => {
    emit('edit-todo', props.index);
};
const deleteHandle = () => {
    emit('delete-todo', props.todoData.id);
};

const checkboxIsClicked = ref(false);
</script>
<template>
    <div class="todo_item_container">
        <input
            type="checkbox"
            class="checkbox"
            :class="{ greenBackground: todoData.isCompleted }"
            :checked="todoData.isCompleted"
            @click="checkboxClickHandle"
        />
        <p :class="{ finished: todoData.isCompleted }" v-if="!todoData.isEditing">{{ todoData.inputValue }}</p>
        <input
            v-else
            class="text"
            :value="todoData.inputValue"
            type="text"
            @input="$emit('update-todo', $event.target.value, index)"
        />
        <div class="icons_container">
            <Icon
                class="icon pencil"
                v-if="!todoData.isEditing"
                @click="editHandle"
                icon="ph:pencil-fill"
                color="#41b080"
                width="22"
            />
            <Icon
                class="icon"
                v-else
                @click="todoData.isEditing = false"
                icon="teenyicons:tick-circle-outline"
                color="#41b080"
                width="22"
            />
            <Icon class="icon trash" @click="deleteHandle" icon="ph:trash" color="#f95e5e" width="22" />
        </div>
    </div>
</template>

<style lang="scss" scoped>
.todo_item_container {
    box-sizing: border-box;
    gap: 0.4rem;
    display: flex;
    align-items: center;
    width: 90vw;
    max-width: 600px;
    height: 30.54px;
    padding: 25px 5px;
    margin-top: 1rem;
    border-radius: 4px;
    overflow: hidden;
    background-color: #c7f9cc;
    &:hover .icon {
        visibility: visible;
    }
    .checkbox {
        appearance: none;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        background-color: white;
        border: 1px solid #41b080;
        transition: border-width 0.2s ease-out;

        .done {
            background-color: #41b080;
        }
        &.greenBackground {
            background-color: #1f8559;
        }
        &:hover {
            cursor: pointer;
            border-width: 2px;
        }
    }
    .text {
        flex: 1;
        height: 25px;
        padding-left: 8px;
        border: 0;
        outline: none;
        color: #22577a;
    }
    p {
        flex: 1;
        color: #22577a;
        padding-left: 0.3rem;
        &.finished {
            text-decoration: line-through;
            text-decoration-color: #f95e5e;
            text-decoration-thickness: 2px;
        }
    }
    .icon {
        visibility: hidden;
        &:hover {
            cursor: pointer;
        }
    }
    .trash {
        margin-left: 0.3rem;
    }
}
</style>
