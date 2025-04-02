<script setup>
const props = defineProps({
    todo: Object
})
</script>

<template>

    <p>
        {{ todo.text }}
    </p>

</template>