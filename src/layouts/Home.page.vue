<template>

<main>

    <co-title h2 
    title="Cosmic Component Library" 
    subtitle="Cosmic is a library of UI components created for Vue 3. The goal is simplicity, readability, and fast prototyping." 
    :classes="title_classes"
    class="space-below" />


    <co-list-examples />
    <div class="large-space" />
    <co-tabs-examples />
    <co-menu-examples />
    <co-card-examples />

</main>

</template>

<script>

import { defineComponent } from 'vue'

import CoTitle from './../components/co-title'
import CoMenuExamples from './../components/examples/co-menu.examples'
import CoCardExamples from './../components/examples/co-card.examples'
import CoTabsExamples from './../components/examples/co-tabs.examples'
import CoListExamples from './../components/examples/co-list.examples'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoMenuExamples,
        CoCardExamples,
        CoTabsExamples,
        CoListExamples,
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
