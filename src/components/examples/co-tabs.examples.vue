<template>
    
<div class="space-below">
    <co-title h3 subtitle="co-tabs are a container for displaying sections of content." :classes="classes">
        <co-badge left="<" content="co-tabs" right=" />" :color="hex.emphasis" />
        co-tabs <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block space-below">
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
</div>


<div class="block space-above">
    <co-tabs :tabs="2" :start-tab="1" :bg="hex.darkbg" shadow-dark>
        <template #label-1>
            <co-title h5 title="Slots" overline="co-tabs" subtitle="required" side :classes="classes" />
        </template>
        <template #label-2>
            <co-title h5 title="Props" overline="co-tabs" subtitle="optional" side :classes="classes" />
        </template>
        <template #panel-1>
            <co-title h6 title="Required Slots" :classes="classes" />
        </template>
        <template #panel-2>
            <co-title h6 title="Required Props" :classes="classes" />
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
import CoCard from './../co-card'

export default defineComponent({

    name: 'co-tabs-examples',

    components: {
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
