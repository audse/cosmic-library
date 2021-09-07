<template>
    
<div class="space-below">
    <co-title h3 subtitle="co-tabs are a container for displaying sections of content." :classes="classes">
        <co-badge left="<" content="co-tabs" right=" />" :color="hex.emphasis" />
        co-menu <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block space-blow">
    <co-card :bg="hex.darkbg" shadow-dark no-spacer :classes="{ before: 'space-above' }">
        <template #before>
            <co-title h5 title="co-tabs Within co-card" />
            <co-tabs :tabs="3" :start-tab="1" :bg="hex.darkgrey" shadow-dark>
                <template #tab-label-1>Tab 1</template>
                <template #tab-panel-1>Tab 1</template>
                <template #tab-label-2>Tab 2</template>
                <template #tab-panel-2>Tab 2</template>
                <template #tab-label-3>Tab 3</template>
                <template #tab-panel-3>Tab 3</template>
            </co-tabs>
        </template>
    </co-card>
</div>

<!-- <div class="block"> -->

<!-- <co-tabs :tabs="3" :start-tab="1" :bg="hex.darkgrey" :inactive-color="hex.darkbg" shadow>
    <template #tab-label-1>
        <co-badge content="New!" :color="hex.emphasis_light" uppercase /> Tab 1
    </template>
    <template #tab-panel-1>Tab 1</template>
    <template #tab-label-2>Tab 2</template>
    <template #tab-panel-2>Tab 2</template>
    <template #tab-label-3>Tab 3</template>
    <template #tab-panel-3>Tab 3</template>
</co-tabs> -->

 <!-- </div> -->

</template>
<script>

import { defineComponent } from 'vue'

import hex from './../../utils/hex.utils'

import CoTabs from './../co-tabs'
import CoTitle from './../co-title'
import CoBadge from './../co-badge'
import CoCard from './../co-card'

export default defineComponent({

    name: 'co-tabs-examples',

    components: {
        CoTabs,
        CoTitle,
        CoBadge,
        CoCard
    },

    setup() {

        const classes = {
            overline: 'co-text-emphasis',
            title: 'co-text',
            subtitle: 'co-text-tint-1'
        }
        
        return {
            classes,
            hex
        }

    },
})
</script>
