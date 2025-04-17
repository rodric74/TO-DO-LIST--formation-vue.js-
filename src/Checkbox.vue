<template>
    <input type="checkbox" @change="onChange">
    <span>{{label}}</span>
</template>

<script setup>
    defineProps({
        label: String
    })
    
   const emits = defineEmits(['check', 'uncheck'])
   const onChange = (event) => {
    if (event.currentTarget.checked) {
        emits('check', event.currentTarget)
    } else {
        emits('uncheck', event.currentTarget)
    }
    }
</script>

<style></style>
