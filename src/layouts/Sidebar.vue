<template>

<div class="sidebar">
    <co-title h5 title="cosmic" subtitle="component library" :classes="title_classes" />

    <div class="space" />
    
    <co-title h6 title="basic elements" overline="components" :classes="title_classes" />
    <co-badge left="<" content="co-textblock" right=" />" :color="emphasis" /><br />
    <co-badge left="<" content="co-title" right=" />" :color="emphasis" /><br />
    <co-badge left="<" content="co-button" right=" />" :color="emphasis" /><br />
    <co-badge left="<" content="co-badge" right=" />" :color="emphasis" /><br />

    <co-title h6 title="layout" overline="components" :classes="title_classes" />
    <co-badge left="<" content="co-card" right=" />" :color="emphasis" /><br />
    <co-badge left="<" content="co-tabs" right=" />" :color="emphasis" /><br />

    <co-title h6 title="navigation" overline="components" :classes="title_classes" />
    <co-badge left="<" content="co-menu" right=" />" :color="emphasis" /><br />

</div>

</template>

<script>

import { defineComponent } from 'vue'

import CoTitle from './../components/co-title'
import CoBadge from './../components/co-badge'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoTitle,
        CoBadge
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