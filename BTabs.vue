<script setup>
import { ref, provide, useSlots } from 'vue'
defineProps({
    small: {
        type: Boolean,
        default: false
    }
})

const tabProvider = ref({
    active: 0,
    count: 0 // her slot bunu bir artiracak ve kendine index yapacak
})

provide('tabProvider', tabProvider)

const slots = useSlots()

const setActive = (val)=>{
    tabProvider.value.active = val
}
</script>
<template>
    <ul class="nav nav-tabs" small>
        <li v-for="(slot, s) in slots.default()" class="nav-item" role="presentation">       
            <button 
                @click="setActive(s)"
                :disabled="slot?.props?.disabled"
                class="nav-link" 
                :class="{'active': tabProvider?.active == s, 'disabled': slot?.props?.disabled}"
                :id="'pane_tab_'+s" 
                data-bs-toggle="tab" 
                :data-bs-target="'#tab_'+s" 
                type="button" 
                role="tab" 
                :aria-controls="'tab_'+s" 
                aria-selected="true">{{slot?.props?.title}}</button> 
        </li>        
    </ul>
    <div class="tab-content">
       <slot/>
    </div>  

</template>
