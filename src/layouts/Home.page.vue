<template>

<main>

    <co-title h2 
    title="Cosmic Component Library" 
    subtitle="Cosmic is a library of UI components created for Vue 3. The goal is simplicity, readability, and fast prototyping." 
    :classes="title_classes"
    class="space-below" />

    <co-text-input v-model="inputA" label="Name" :outline-color="hex.emphasis" :text-color="hex.white" placeholder="Enter your name" width="100%" /><br />
    <co-text-input v-model="inputB" label="Email" :bg="hex.darkergrey" :text-color="hex.white" placeholder="Enter your email" width="100%" /><br />
    <co-text-input v-model="inputC" label="Phone Number" :outline-color="hex.emphasis" :text-color="hex.white" placeholder="Enter your name" material width="100%" /><br />


    <div class="hidden">
        <co-list-examples />
        <div class="large-space" />
        <co-tabs-examples />
        <co-menu-examples />
        <co-card-examples />
    </div>

</main>

</template>

<script>

import { defineComponent, ref } from 'vue'

import hex from './../utils/hex.utils'

import CoTitle from './../components/co-title'
import CoMenuExamples from './../components/examples/co-menu.examples'
import CoCardExamples from './../components/examples/co-card.examples'
import CoTabsExamples from './../components/examples/co-tabs.examples'
import CoListExamples from './../components/examples/co-list.examples'
import CoTextInput from './../components/co-textinput'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoMenuExamples,
        CoCardExamples,
        CoTabsExamples,
        CoListExamples,
        CoTitle,
        CoTextInput,
    },

    setup () {

        const inputA = ref('')
        const inputB = ref('')
        const inputC = ref('input c')

        const title_classes = {
            title: 'co-text',
            subtitle: 'co-text-tint-3'
        }

        return {
            inputA,
            inputB,
            inputC,
            title_classes,
            hex
        }

    }

})

</script>
<style>

.hidden {
    display: none;
}

</style>
