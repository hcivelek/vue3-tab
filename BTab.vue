<script setup>

import { ref, inject, watch, onBeforeMount } from 'vue'

const props = defineProps({
    title: String,
    active: {
        type: Boolean,
        default: false
    },    
    disabled: {
        type: Boolean,
        default: false
    }    
})

const index = ref(0);

const isActive = ref(props?.active ?? false);

const tabProvider = inject("tabProvider");

watch(
    ()=>tabProvider.value.active,
    (val) => {
        isActive.value = index.value === val;
    }
);

onBeforeMount(() => {
    index.value = tabProvider.value.count;
    tabProvider.value.count++;
    isActive.value = index.value === tabProvider.value.active;
});



</script>
<template>
<div class="tab-pane fade" :class="{'show active': tabProvider?.active == index}"  role="tabpanel" tabindex="0">
    <slot/>
</div>
</template>
