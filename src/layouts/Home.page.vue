<template>

<div class="container">

    <Title h2 
    title="Cosmic Component Library" 
    subtitle="Cosmic is a library of UI components created for Vue 3. The goal is simplicity, readability, and fast prototyping." 
    :classes="title_classes"
    class="space-below" />

    <CoCardExamples />

</div>

</template>

<script>

import { defineComponent } from 'vue'

import Title from './../components/co-title'
import CoCardExamples from './../components/examples/co-card.examples'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoCardExamples,
        Title
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
