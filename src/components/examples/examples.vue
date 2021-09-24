<template>
    
 
<div class="space-below">
    <co-title h3 :subtitle="subtitle" :classes="classes">
        <co-badge left="<" :content="component" right=" />" :color="hex.emphasis" />
        {{ component }} <span class="co-text-tint-1">component</span>
    </co-title>
</div>


<article class="space-below">
    <slot></slot>
</article>


<div class="block space-above">
    <co-tabs :tabs="5" :start-tab="1" :bg="hex.darkbg" shadow-dark>
        <template #label-1>
            <co-title h6 title="Slots" :classes="classes" />
        </template>
        <template #label-2>
            <co-title h6 title="Scoped Slots" :classes="classes" />
        </template>
        <template #label-3>
            <co-title h6 title="Props" :classes="classes" />
        </template>
        <template #label-4>
            <co-title h6 title="Emits" :classes="classes" />
        </template>
        <template #label-5>
            <co-title h6 title="Class Object" :classes="classes" />
        </template>

        <template #panel-1>
            <section>
                <slot name="slots"></slot>
            </section>
        </template>
        <template #panel-2>
            <section>
                <slot name="scoped"></slot>
            </section>
        </template>
        <template #panel-3>
            <section>
                <slot name="props"></slot>
            </section>
        </template>
        <template #panel-4>
            <section>
                <slot name="emits"></slot>
            </section>
        </template>
        <template #panel-5>
            <section>
                <slot name="classes"></slot>
            </section>
        </template>
    </co-tabs>
</div>

</template>
<script>

import { defineComponent } from 'vue'

import hex from './../../utils/hex.utils'

import CoTabs from './../co-tabs.vue'
import CoTitle from './../co-title.vue'
import CoBadge from './../co-badge.vue'

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

    setup ( ) {

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
