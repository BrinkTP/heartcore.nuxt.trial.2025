
<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  type: {
    type: String,
    default: 'button'
  },
  disabled: {
    type: Boolean,
    default: false
  },
  loading: {
    type: Boolean,
    default: false
  },
  variant: {
    type: String,
    default: 'primary' // could be 'primary', 'secondary', etc.
  }
})

const emits = defineEmits(['click'])

function handleClick(event) {
  if (!props.disabled && !props.loading) {
    emits('click', event)
  }
}
</script>
<template>
    <button
      :type="type"
      :disabled="disabled || loading"
      :class="['tp-button', variant, { loading }]"
      @click="handleClick"
    >
      <span v-if="loading" class="spinner" />
      <slot />
    </button>
  </template>
  
  
  <style scoped>
  .tp-button {
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background 0.2s ease-in-out;
  }
  
  .tp-button.primary {
    background-color: #007bff;
    color: white;
  }
  
  .tp-button.secondary {
    background-color: #6c757d;
    color: white;
  }
  
  .tp-button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }
  
  .spinner {
    border: 2px solid transparent;
    border-top-color: white;
    border-radius: 50%;
    width: 1em;
    height: 1em;
    margin-right: 0.5em;
    display: inline-block;
    animation: spin 1s linear infinite;
    vertical-align: middle;
  }
  
  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
  </style>
  