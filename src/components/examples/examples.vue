<template>
    
 
<div class="space-below">
    <co-title h3 :subtitle="subtitle" :classes="classes">
        <co-badge left="<" :content="component" right=" />" :color="hex.emphasis" />
        {{ component }} <span class="co-text-tint-1">component</span>
    </co-title>
</div>


<div class="block space-below">
    <slot></slot>
</div>


<div class="block space-above">
    <co-tabs :tabs="3" :start-tab="1" :bg="hex.darkbg" shadow-dark>
        <template #label-1>
            <co-title h6 title="Slots" :overline="component" :classes="classes" />
        </template>
        <template #label-2>
            <co-title h6 title="Props" :overline="component" :classes="classes" />
        </template>
        <template #label-3>
            <co-title h6 title="Class Object" :overline="component" :classes="classes" />
        </template>

        <template #panel-1>

            <slot name="slots"></slot>

        </template>
        <template #panel-2>

            <slot name="props"></slot>

        </template>
        <template #panel-3>

            <slot name="classes"></slot>

        </template>
    </co-tabs>
</div>

</template>
<script>

import { defineComponent } from 'vue'

import hex from './../../utils/hex.utils'

import CoTabs from './../co-tabs'
import CoTitle from './../co-title'
import CoBadge from './../co-badge'

export default defineComponent({

    name: 'Examples',

    components: {
        CoTabs,
        CoTitle,
        CoBadge,
    },

    props: {
        component: String,
        subtitle: String,
    },

    setup () {

        const classes = {
            overline: 'co-text-emphasis',
            title: 'co-text',
            subtitle: 'co-text-tint-2'
        }
        
        return {
            classes,
            hex
        }
        
    },
})

</script>
