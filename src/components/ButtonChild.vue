<script setup>
    defineEmits(['clique'])
</script>

<template>
    <li>
        <button @click.prevent="$emit('clique')" >
            <slot>

            </slot>
        </button>
    </li>
</template>

<style scoped>

</style>