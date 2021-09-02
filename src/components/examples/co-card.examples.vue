<template>

<div class="space-below">
    <Title h3 subtitle="CoCards are a general-purpose container for content." :classes="classes">
        <Badge content="co-card" :color="emphasis_light" large />
    </Title>
</div>

<div class="block">
    <Card :classes="classes" shadow-dark>
        <LoremIpsum add="2s" />
        <template #toolbar>
            <Button label="Toolbar" :color="grey" subtle uppercase sm />
        </template>
        <template #toolbar-right>
            <Badge content="toolbar-right" :color="white" uppercase />
        </template>
        <template #header>
            <Title h4 title="Header (using co-title)" overline="overline" :classes="classes">
                <template #subtitle>Subtitle - <LoremIpsum add="5-10w" /></template>
            </Title>
        </template>
        <template #header-right>
            <Badge content="header-right" :color="white" uppercase />
        </template>
        <template #before>
            <Button label="before-content" :color="emphasis" subtle sm uppercase /> <LoremIpsum add="5w" />
        </template>
        <template #actions>
            <Button label="Actions" :color="emphasis" subtle sm />
        </template>
        <template #actions-right>
            <Button label="Actions-Right" :color="emphasis" :text-color="truewhite" filled />
        </template>
    </Card>
</div>

<div class="block">
    <Card :classes="classes" shadow-dark>
        <template #header>
            <Title h5 title="My Second Card" :classes="classes">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </Title>
        </template>
        <template #header-right>
            <Button :color="grey" round light sm>
                <i class="gg-close" :style="{color: white}" />
            </Button>
        </template>
        <template #before-content>
            <Button label="&times;" :color="grey" light />
        </template>
    </Card>

    <Card :classes="{ card: 'co-bg', card: 'co-bg-mixemphasis'}" shadow-dark>
        <template #header>
            <Badge content="incomplete" :color="truewhite" subtle sm />
            <Badge content="new" :color="emphasis_light" subtle sm />
            <Title h5 title="My Third Card" :classes="{title: 'co-text-truewhite', subtitle: 'co-text-emphasis-text'}">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </Title>
        </template>
    </Card>
</div>
<div class="block">
    <Card :classes="{ before: 'co-bg-body-background block-center co-border-drag-drop' }" no-spacer shadow-dark>
        <template #before>
            <div class="flex co-center">Empty Card using <Badge content="before" :color="white" />slot and <Badge content="no-spacer" :color="grey" /> prop.</div>
        </template>
    </Card>
</div>

<div class="block space-below">
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark>
        <template #header><Title title="Option A" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option A" />
        </template>
    </Card>
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark>
        <template #header><Title title="Option B" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option B" :color="emphasis" subtle />
        </template>
    </Card>
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark>
        <template #header><Title title="Option C" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option C" :color="emphasis" filled :text-color="truewhite" />
        </template>
    </Card>
</div>

<TextBlock>

<Title h6 title="Slots" overline="co-card" subtitle="each slot is optional. The card will add space only for the needed slots." side :classes="classes" />

<div class="block">
    <div class="aside">
        <Badge content="toolbar" :color="white" /><Badge content="toolbar-right" :color="white" />
    </div>
    <div class="flex co-text-tint-1">
        Are within the upper padding. Generally used for buttons, labels, etc.
    </div>
</div>


<div class="block">
    <div class="aside">
        <Badge content="header" :color="white" /><Badge content="header-right" :color="white" />
    </div>
    <div class="flex co-text-tint-1">
        Make up the main title block.
    </div>
</div>


<div class="block">
    <div class="aside">
        <Badge content="before" :color="white" />
    </div>
    <div class="flex co-text-tint-1">
        Is a special section without padding: useful for alerts/warnings. Use in conjunction with <Badge content="no-spacer" :color="grey" /> to create an 'empty' card.
    </div>
</div>

<div class="block">
    <div class="aside">
        <Badge content="default" />
    </div>
    <div class="flex co-text-tint-1">
        is the main content block, with padding.
    </div>
</div>

<div class="block">
    <div class="aside">
        <Badge content="actions" :color="white" />
        <Badge content="actions-right" :color="white" />
    </div>
    <div class="flex co-text-tint-1">
        contain the buttons/actions for the card, within the lower padding.
    </div>
</div>

<Title h6 title="Props" overline="co-card" subtitle="Each prop is optional. By default, they are all disabled." side :classes="classes" />

<div class="block">
    <div class="aside">
        <Badge content="no-margin" :color="white" />
        <Badge content="boolean" :color="grey" />
    </div>
    <div class="flex co-text-tint-1">
        removes the default margin surrounding each card.
    </div>
</div>
<div class="block">
    <div class="aside">
        <Badge content="no-spacer" :color="white" />
        <Badge content="boolean" :color="grey" />
    </div>
    <div class="flex co-text-tint-1">
        removes the extra padding from the top/bottom border radius.
    </div>
</div>
<div class="block">
    <div class="aside">
        <Badge content="shadow" :color="white" />
        <Badge content="shadow-light" :color="white" />
        <Badge content="shadow-dark" :color="white" />
        <Badge content="boolean" :color="grey" />
    </div>
    <div class="flex co-text-tint-1">
        adds a subtle drop shadow. Choose only one of the three. <Badge content="shadow-light" :color="grey" /> is optimized for light backgrounds, while  <Badge content="shadow-dark" :color="grey" /> is optimized for dark mode.
    </div>
</div>
<div class="block">
    <div class="aside">
        <Badge content="dense" :color="white" />
        <Badge content="boolean" :color="grey" />
    </div>
    <div class="flex co-text-tint-1">
        reduces the overall size.
    </div>
</div>

<Title h6 title="Class Object" />

</TextBlock>

</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import Badge from './../co-badge'
import Button from './../co-button'
import Title from './../co-title'
import Card from './../co-card'
import TextBlock from './../co-textblock'

export default defineComponent({
    
    name: 'CoCardExamples',

    components: {
        LoremIpsum,
        Title,
        Card,
        Badge,
        Button,
        TextBlock,
    },

    setup () {

        const emphasis = '#da4790'
        const emphasis_light = '#ee96c2'
        const truewhite = '#ffffff'
        const white = '#a9b6c5'
        const grey = '#7d8894'

        const classes = {
            card: 'co-bg',
            before: 'co-padding co-bg-lightemphasis co-text-emphasis-text',
            overline: 'co-text-emphasis',
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
            classes
        }
    }

})

</script>
<style lang="scss" scoped>

.block {
    margin: 1.25em 0;
}

.aside {
    width: 150px;
    text-align: right;
    margin-right: 1em;
}

</style>