<script setup lang="ts">
import ChildComp from './ChildComp.vue'

const message = ref(null);

</script>

<template>
   <div>
      <h2>This is ParentComp</h2>
      <ChildComp message="test message" @response="(childResponse) => message = childResponse"/>
      <h3>Message from Child: {{ message || 'No response yet'}}</h3>
   </div>
</template>
