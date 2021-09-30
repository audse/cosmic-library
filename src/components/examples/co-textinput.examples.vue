<script lang="ts" setup>

import examples from './examples.vue'
import CoTextInput from './../co-textinput.vue'

import { ref } from 'vue'
import hex from './../../utils/hex.utils'

const inputA = ref('')
const inputB = ref('Audrey')
const inputC = ref('audrey@audreyserene.com')

</script>
<template>
    
<examples component="co-text-input" subtitle="co-text-input is a generic text input field.">

<co-text-input v-model="inputA" label="Input" :outline-color="hex.emphasis" material />
<co-text-input v-model="inputB" label="Name" :outline-color="hex.emphasis" placeholder="Your Name" />
<co-text-input v-model="inputC" label="Email" :text-color="hex.white" :bg="hex.darkgrey" placeholder="Your Email" width="100%" />


</examples>

</template>