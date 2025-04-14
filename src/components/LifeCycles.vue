<script setup lang="ts">
import { onMounted, ref, type Ref, type VNodeRef, watch } from 'vue'

const textElementRef: Ref<HTMLElement | null> = ref(null);
const todoId = ref(1)
const todoData = ref(null)

onMounted(() => {
    fetchData()
    if (textElementRef.value) {
        textElementRef.value.textContent = 'Hello World! (changed onMounted)'; // Access the DOM element directly
    }
});

async function fetchData() {
    todoData.value = null
    const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    todoData.value = await res.json()
}

watch(todoId, (newCount: number) => {
    fetchData()
})
</script>
<template>
    <div>
    <p ref="textElementRef">Change after onMounted longer text test 123 Does this keep growing</p>

    <div class="py-5">
        <p>Todo id: {{ todoId }}</p>
        <button @click="todoId++" :disabled="!todoData">Fetch next todo</button>
        <p v-if="!todoData">Loading...</p>
        <pre v-else>{{ todoData }}</pre>
    </div>
</div>
</template>
<style scoped>
p {
    color: red;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    margin-top: 20px;
}

.py-5 {
    padding-top: 5rem;
    padding-bottom: 5rem;
}
</style>