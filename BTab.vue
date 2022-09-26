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

const setActive = ()=>{
    if(!props?.disabled){
        tabProvider.value.active = index.value
    }
}

</script>
<template>
    <li class="nav-item" @click="setActive">        
        <a class="nav-link" :class="{'active': isActive, 'disabled':disabled}" aria-current="page" href="#">{{title}}</a>
    </li>
</template>
