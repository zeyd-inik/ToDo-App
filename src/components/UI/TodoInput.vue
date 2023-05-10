<script setup>
import { ref } from 'vue';

const emit = defineEmits(['create-todo']);

const input = ref('');
const invalid = ref(false);
const errorMessage = ref('');

const animated_p = ref(null);

const clickHandle = () => {
    if (input.value !== '') {
        emit('create-todo', input.value);
        input.value = '';
        return;
    }
    invalid.value = true;
    errorMessage.value = 'Todo value cannot be empty!';
    setTimeout(() => {
        invalid.value = false;
        errorMessage.value = '';
        animated_p.value.style.display = 'none';
    }, 3000);
};
</script>
<template>
    <div class="input_container">
        <input type="text" v-model="input" />
        <button class="btn" @click="clickHandle">Create</button>
    </div>
    <Transition name="error_animation">
        <p ref="animated_p" class="error_text" v-if="errorMessage">{{ errorMessage }}</p>
    </Transition>
</template>

<style lang="scss" scoped>
/* animation */

.error_animation-leave-from {
    opacity: 1;
}
.error_animation-leave-to {
    opacity: 0;
}
.error_animation-leave-active {
    transition: all 2s ease;
}

.input_container {
    display: flex;
    align-items: center;
    width: 90vw;
    max-width: 600px;
    height: 30.54px;
    border-radius: 4px;
    overflow: hidden;

    input[type='text'] {
        flex: 1;
        height: 100%;
        border: 0;
        padding-left: 1rem;
        outline: none;
        color: #22577a;
    }
    .btn {
        width: 60px;
        height: 100%;
        border: 0;
        outline: none;
        color: #7fa9d3;
        background-color: #c7f9cc;
        letter-spacing: 0.6px;
        font-weight: 600;
        &:hover {
            cursor: pointer;
        }
        &:active {
            transform: scale(0.98);
            font-size: 14px;
        }
    }
}
.error_text {
    text-align: center;
    color: #f95e5e;
    font-size: small;
    margin-top: 0.7rem;
}
</style>
