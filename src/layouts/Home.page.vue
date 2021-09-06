<template>

<div class="container">

    <co-title h2 
    title="Cosmic Component Library" 
    subtitle="Cosmic is a library of UI components created for Vue 3. The goal is simplicity, readability, and fast prototyping." 
    :classes="title_classes"
    class="space-below" />


    <co-tabs-examples />

    <!-- <div class="hidden"> -->
        <div class="large-space" />
        <co-menu-examples />


        <co-card-examples />
    <!-- </div> -->

</div>

</template>

<script>

import { defineComponent } from 'vue'

import CoTitle from './../components/co-title'
import CoMenuExamples from './../components/examples/co-menu.examples'
import CoCardExamples from './../components/examples/co-card.examples'
import CoTabsExamples from './../components/examples/co-tabs.examples'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoMenuExamples,
        CoCardExamples,
        CoTabsExamples,
        CoTitle
    },

    setup () {

        const title_classes = {
            title: 'co-text',
            subtitle: 'co-text-tint-3'
        }

        return {
            title_classes
        }

    }

})

</script>
<style>

.hidden {
    display: none;
}

</style>
