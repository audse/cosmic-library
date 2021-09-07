<template>
    
<examples component="co-tabs" subtitle="co-tabs are a container for displaying sections of content.">

    <!-- Examples -->
    <co-card :bg="hex.darkbg" shadow-dark no-spacer :classes="{ before: 'space-above' }">
        <template #before>
            <co-title h5 class="co-padding">
                <co-badge left="<" content="co-tabs" right=" />" :color="hex.white" />
                fits nicely within 
                <co-badge left="<" content="co-card" right=" />" :color="hex.white" />
            </co-title>
            <co-tabs :tabs="3" :start-tab="1" :bg="hex.darkgrey" shadow-dark>
                <template #label-1>Tab 1</template>
                <template #panel-1>Tab 1</template>
                <template #label-2>Tab 2</template>
                <template #panel-2>Tab 2</template>
                <template #label-3>Tab 3</template>
                <template #panel-3>Tab 3</template>
            </co-tabs>
        </template>
    </co-card>

    <!-- Slots -->
    <template #slots>
        <co-title h6 title="Required Slots" :classes="classes" />

        <p><co-badge left="#" content="label-n" :color="hex.white" /></p>

        <p><co-badge left="#" content="panel-n" :color="hex.white" /></p>
    </template>

    <!-- Props -->
    <template #props>
        <co-title h6 title="Required Props" :classes="classes" />

        <p>
            <co-badge content="int" :color="hex.emphasis" />
            <co-badge content="tabs" :color="hex.white" />
        </p>

        <co-title h6 title="Optional Props" :classes="classes" />

        <p>
            <co-badge content="int" :color="hex.emphasis" />
            <co-badge content="start-tab" :color="hex.white" />
        </p>
        <p>
            <co-badge content="string" :color="hex.emphasis" />
            <co-badge content="bg" :color="hex.white" />
        </p>
        <p>
            <co-badge content="boolean" :color="hex.emphasis" />
            <co-badge content="shadow" :color="hex.white" />
            <co-badge content="shadow-light" :color="hex.white" />
            <co-badge content="shadow-dark" :color="hex.white" />
        </p>
        <p>
            <co-badge content="boolean" :color="hex.emphasis" />
            <co-badge content="less-round" :color="hex.white" />
        </p>
    </template>

    <!-- Class Object -->
    <template #classes>
        ...
    </template>

</examples>


</template>
<script>

import { defineComponent } from 'vue'

import hex from './../../utils/hex.utils'

import Examples from './examples'
import CoTabs from './../co-tabs'
import CoTitle from './../co-title'
import CoBadge from './../co-badge'
import CoCard from './../co-card'

export default defineComponent({

    name: 'co-tabs-examples',

    components: {
        Examples,

        CoTabs,
        CoTitle,
        CoBadge,
        CoCard,
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
