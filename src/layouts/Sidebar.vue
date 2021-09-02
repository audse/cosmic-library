<template>

<div class="sidebar">
    <Title h5 title="cosmic" subtitle="component library" :classes="title_classes" />

    <div class="space" />
    
    <Title h6 title="basic elements" overline="components" :classes="title_classes" />
    <Badge left="<" content="co-textblock" right=" />" :color="emphasis" /><br />
    <Badge left="<" content="co-title" right=" />" :color="emphasis" /><br />
    <Badge left="<" content="co-button" right=" />" :color="emphasis" /><br />
    <Badge left="<" content="co-badge" right=" />" :color="emphasis" /><br />

    <Title h6 title="layout" overline="components" :classes="title_classes" />
    <Badge left="<" content="co-card" right=" />" :color="emphasis" /><br />

</div>

</template>

<script>

import { defineComponent } from 'vue'

import Title from './../components/co-title'
import Badge from './../components/co-badge'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        Title,
        Badge
    },

    setup () {

        const title_classes = {
            title: 'co-text',
            subtitle: 'co-text-tint-2',
            overline: 'co-text-emphasis-text'
        }

        const emphasis = '#da4790';

        return {
            title_classes,
            emphasis
        }

    }

})

</script>

<style scoped>

.space {
    width: 100%;
    height: 1.5em;
}

</style>