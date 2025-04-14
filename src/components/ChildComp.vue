<script setup lang="ts">
const props = defineProps({
   message: String
})

const emit = defineEmits(['response'])

</script>

<template>
   <h2>This is ChildComp</h2>
   <h3>Message: {{ message || 'No props passed yet'}}</h3>
   <button @click="$emit('response', 'This is a response from ChildComp')">Send Response</button>
</template>
