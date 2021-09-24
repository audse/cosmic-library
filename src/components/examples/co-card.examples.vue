<template>

<examples component="co-card" subtitle="co-cards are a general-purpose container for content.">

    <!-- Examples -->
    <section>
        <co-card :bg="bg" :classes="classes" shadow-dark>
            <LoremIpsum add="2s" />
            <template #toolbar>
                <co-badge content="Toolbar" :color="grey" subtle uppercase sm />
            </template>
            <template #toolbar-right>
                <co-badge content="toolbar-right" :color="white" uppercase sm />
            </template>
            <template #header>
                <co-title h4 overline="overline" :classes="classes">
                    Header (using co-title)
                    <template #subtitle>Subtitle - <LoremIpsum add="5-10w" /></template>
                </co-title>
            </template>
            <template #header-right>
                <co-badge content="header-right" :color="white" uppercase />
            </template>
            <template #before>
                <co-button label="before" :color="emphasis" subtle sm uppercase /> <LoremIpsum add="5w" />
            </template>
            <template #actions>
                <co-button label="Actions" :color="emphasis" subtle sm />
            </template>
            <template #actions-right>
                <co-button label="Actions-Right" :color="emphasis" :label-color="truewhite" filled />
            </template>
        </co-card>
    </section>

    <section class="flex">
        <co-card :bg="bg" :classes="classes" shadow-dark >
            <template #header>
                <co-title h5 title="My Second co-card" :classes="classes">
                    <template #subtitle><LoremIpsum add="4-8w" /></template>
                </co-title>
            </template>
            <template #header-right>
                <co-button :color="grey" round light sm>
                    <i class="gg-close" :style="{color: white}" />
                </co-button>
            </template>
        </co-card>

        <co-card :bg="emphasis" :classes="{ card: 'co-bg', card: 'co-bg-mixemphasis'}" shadow-dark >
            <template #header>
                <co-title h5 title="My Third co-card" :classes="{title: 'co-text-truewhite', subtitle: 'co-text-emphasis-text'}">
                    <template #subtitle><LoremIpsum add="4-8w" /></template>
                </co-title>
                <co-badge content="incomplete" :color="truewhite" subtle sm />
                <co-badge content="new" :color="emphasis_light" subtle sm />
            </template>
        </co-card>
    </section>
    <section>
        <co-card :classes="{ before: 'co-bg-body-background block-center co-border-drag-drop' }" no-spacer shadow-dark>
            <template #before>
                <div class="flex co-center">Empty co-card using <co-badge content="before" :color="white" />slot and <co-badge content="no-spacer" :color="grey" /> prop.</div>
            </template>
        </co-card>
    </section>

    <section class="block">
        <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark >
            <template #header><co-title title="Option A" /></template>
            <LoremIpsum add="10w" />
            <template #actions>
                <co-button label="Option A" :color="white" subtle />
            </template>
        </co-card>
        <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark >
            <template #header><co-title title="Option B" /></template>
            <LoremIpsum add="10w" />
            <template #actions>
                <co-button label="Option B" :color="emphasis" outline />
            </template>
        </co-card>
        <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark >
            <template #header><co-title title="Option C" /></template>
            <LoremIpsum add="10w" />
            <template #actions>
                <co-button label="Option C" :color="emphasis" filled :label-color="truewhite" />
            </template>
        </co-card>
    </section>

    <!-- Slots -->
    <template #slots>

        <p><co-badge left="#" content="default" /></p>


        <p><co-badge left="#" content="toolbar" :color="white" /><co-badge left="#" content="toolbar-right" :color="white" /></p>


        <p><co-badge left="#" content="header" :color="white" /><co-badge left="#" content="header-right" :color="white" /></p>


        <p>
            <co-badge left="#" content="before" :color="white" />
            Use in conjunction with <co-badge content="no-spacer" :color="grey" sm /> to create an 'empty' card.
        </p>


        <p>
            <co-badge left="#" content="actions" :color="white" />
            <co-badge left="#" content="actions-right" :color="white" />
            These slots are semantic- wrapper in footer and nav tags, respectively.
        </p>

        <div class="space-below" />
    </template>

    <!-- Props -->
    <template #props>

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="no-spacer" :color="white" />
        </p>


        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="shadow" :color="white" />
            <co-badge content="shadow-light" :color="white" />
            <co-badge content="shadow-dark" :color="white" />

            choose <co-badge content="shadow-light" :color="grey" sm /> for light backgrounds, or <co-badge content="shadow-dark" :color="grey" sm /> for dark backgrounds.
        </p>


        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="dense" :color="white" />
        </p>


        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="less-round" :color="white" />
        </p>

    </template>
</examples>

</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import CoBadge from './../co-badge.vue'
import CoButton from './../co-button.vue'
import CoTitle from './../co-title.vue'
import CoCard from './../co-card.vue'
import Examples from './examples.vue'

export default defineComponent({
    
    name: 'co-card-examples',

    components: {
        LoremIpsum,

        Examples,

        CoTitle,
        CoCard,
        CoBadge,
        CoButton,
    },

    setup () {

        const emphasis = '#da4790'
        const emphasis_light = '#ee96c2'
        const truewhite = '#ffffff'
        const white = '#a9b6c5'
        const grey = '#7d8894'
        const bg = '#303542'
        const darkbg = '#1d212b'

        const classes = {
            container: 'co-margin-sm',
            card: 'co-bg',
            before: 'co-padding co-bg-lightemphasis co-text-emphasis-text',
            overline: 'co-text-emphasis',
            title: 'co-text',
            subtitle: 'co-text-tint-2',
            actions: 'co-bg-lightgrey',
            content: 'co-text-tint-1',
        }

        return {
            emphasis,
            emphasis_light,
            truewhite,
            white,
            grey,
            bg,
            darkbg,
            classes
        }
    }

})

</script>
<style lang="scss" scoped>

.block {
    margin: 0.5em 0;
    display: flex;
    align-items: center;
}
</style>