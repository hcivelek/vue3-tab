<script setup>
import { ref, provide } from 'vue'

const tabProvider = ref({
    active: 0,
    count: 0 // every slot will increase this and set it as its own index.
})

provide('tabProvider', tabProvider)

</script>
<template>
    <ul class="nav nav-tabs">
        <slot />
    </ul>
</template>
