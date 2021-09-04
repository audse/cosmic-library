<template>

<div class="space-below">
    <co-title h3 subtitle="co-cards are a general-purpose container for content." :classes="classes">
        <co-badge left="<" content="co-card" right=" />" :color="emphasis" />
        co-card <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block">
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
            <co-button label="before-content" :color="emphasis" subtle sm uppercase /> <LoremIpsum add="5w" />
        </template>
        <template #actions>
            <co-button label="Actions" :color="emphasis" subtle sm />
        </template>
        <template #actions-right>
            <co-button label="Actions-Right" :color="emphasis" :text-color="truewhite" filled />
        </template>
    </co-card>
</div>

<div class="block">
    <co-card :bg="bg" :classes="classes" shadow-dark margin-lg>
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
        <template #before-content>
            <co-button label="&times;" :color="grey" light />
        </template>
    </co-card>

    <co-card :bg="emphasis" :classes="{ card: 'co-bg', card: 'co-bg-mixemphasis'}" shadow-dark margin-lg>
        <template #header>
            <co-title h5 title="My Third co-card" :classes="{title: 'co-text-truewhite', subtitle: 'co-text-emphasis-text'}">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </co-title>
            <co-badge content="incomplete" :color="truewhite" subtle sm />
            <co-badge content="new" :color="emphasis_light" subtle sm />
        </template>
    </co-card>
</div>
<div class="block">
    <co-card :classes="{ before: 'co-bg-body-background block-center co-border-drag-drop' }" no-spacer shadow-dark>
        <template #before>
            <div class="flex co-center">Empty co-card using <co-badge content="before" :color="white" />slot and <co-badge content="no-spacer" :color="grey" /> prop.</div>
        </template>
    </co-card>
</div>

<div class="block space-below">
    <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><co-title title="Option A" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <co-button label="Option A" :color="white" subtle />
        </template>
    </co-card>
    <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><co-title title="Option B" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <co-button label="Option B" :color="emphasis" outline />
        </template>
    </co-card>
    <co-card :bg="darkbg" :classes="{ card: 'co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><co-title title="Option C" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <co-button label="Option C" :color="emphasis" filled :text-color="truewhite" />
        </template>
    </co-card>
</div>


<co-textblock class="co-text-tint-1">

<co-title h5 title="Slots" overline="co-card" subtitle="each slot is optional. The card will add space only for the needed slots." side :classes="classes" />

<div class="block space-above">
    <co-badge left="#" content="default" />
</div>


<div class="block space-above">
    <co-badge left="#" content="toolbar" :color="white" /><co-badge left="#" content="toolbar-right" :color="white" />
</div>


<div class="block space-above">
    <co-badge left="#" content="header" :color="white" /><co-badge left="#" content="header-right" :color="white" />
</div>


<div class="block space-above">
    <co-badge left="#" content="before" :color="white" />

    Use in conjunction with <co-badge content="no-spacer" :color="grey" sm /> to create an 'empty' card.
</div>


<div class="block space-above">
    <co-badge left="#" content="actions" :color="white" />
    <co-badge left="#" content="actions-right" :color="white" />
</div>

<div class="space-below" />

<co-title h5 title="Props" overline="co-card" subtitle="Each prop is optional. By default, they are all disabled." side :classes="classes" />

<div class="block space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="no-margin" :color="white" />
    <co-badge content="margin-sm" :color="white" />
    <co-badge content="margin-lg" :color="white" />
</div>


<div class="block space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="no-spacer" :color="white" />
</div>


<div class="block space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="shadow" :color="white" />
    <co-badge content="shadow-light" :color="white" />
    <co-badge content="shadow-dark" :color="white" />

    choose <co-badge content="shadow-light" :color="grey" sm /> for light backgrounds, or <co-badge content="shadow-dark" :color="grey" sm /> for dark backgrounds.
</div>


<div class="block space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="dense" :color="white" />
</div>


<div class="block space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="less-round" :color="white" />
</div>

<div class="space-above" />

<co-title h5 title="Class Object" overline="co-card" :classes="classes" />

</co-textblock>

</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import CoBadge from './../co-badge'
import CoButton from './../co-button'
import CoTitle from './../co-title'
import CoCard from './../co-card'
import CoTextblock from './../co-textblock'

export default defineComponent({
    
    name: 'co-card-examples',

    components: {
        LoremIpsum,
        CoTitle,
        CoCard,
        CoBadge,
        CoButton,
        CoTextblock,
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