<template>
    <label>
      <input type="checkbox" :checked="modelValue" @change="$emit('update:modelValue', $event.target.checked)">
      <span>{{ label }}</span>
    </label>
  </template>
  
  <script setup>
  defineProps({
    label: String,
    modelValue: Boolean
  })
  defineEmits(['update:modelValue'])
  </script>