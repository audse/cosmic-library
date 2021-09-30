<template>
    
<examples component="co-list" subtitle="co-lists are a way of cleanly displaying data.">

    <!-- Examples -->
    <co-list :border-color="hex.darkbg" ripple-dark>
        <co-list-item tabindex="0">
            <template #left>
                <co-badge content="left" :color="hex.emphasis" />
            </template>

            <co-title h6 title="List Item 1" :classes="classes">
                <template #subtitle>
                    <LoremIpsum add="1s" />
                </template>
            </co-title>

            <template #right>
                <co-badge content="right" :color="hex.emphasis" />
            </template>
        </co-list-item>
        <co-list-item tabindex="0">
            <co-title h6 title="List Item 2" :classes="classes">
                <template #subtitle>
                    <LoremIpsum add="1s" />
                </template>
            </co-title>
        </co-list-item>
    </co-list>

    <co-card :bg="hex.darkbg">
        <template #header>
            <co-title h4 title="All Users" subtitle="This is an example list of all the users." :classes="classes" />
        </template>
        <template #before>
            <co-list ripple-dark>
                <co-list-item tabindex="0">
                    <template #left><co-avatar :bg="hex.emphasis">JS</co-avatar></template>
                    John Smith 
                    <template #right><co-badge content="johnsmith" right="@company.com" :color="hex.white" /></template>
                </co-list-item>
                <co-list-item tabindex="0">
                    <template #left><co-avatar :bg="hex.emphasis">SM</co-avatar></template>
                    Sarah Michaels
                    <template #right><co-badge content="sarahmichaels" right="@company.com" :color="hex.white" /></template>
                </co-list-item>
                <co-list-item tabindex="0">
                    <template #left><co-avatar :bg="hex.emphasis">GR</co-avatar></template>
                    George Ramirez
                    <template #right><co-badge content="georgeramirez" right="@company.com" :color="hex.white" /></template>
                </co-list-item>
            </co-list>
        </template>
    </co-card>

    <!-- Slots -->
    <template #slots>
    </template>

    <!-- Props -->
    <template #props>
    </template>

    <!-- Class Object -->
    <template #classes>
        ...
    </template>

</examples>


</template>
<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import hex from './../../utils/hex.utils'

import Examples from './examples.vue'
import CoList from './../co-list.vue'
import CoListItem from './../co-listitem.vue'
import CoTitle from './../co-title.vue'
import CoBadge from './../co-badge.vue'
import CoCard from './../co-card.vue'
import CoAvatar from './../co-avatar.vue'

export default defineComponent({

    name: 'co-list-examples',

    components: {
        LoremIpsum,
        Examples,
        CoList,
        CoListItem,

        // CoTabs,
        CoTitle,
        CoBadge,
        CoCard,
        CoAvatar
    },

    setup() {

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
