<template>

<div class="space-below">
    <Title h3 subtitle="CoCards are a general-purpose container for content." :classes="classes">
        <Badge content="co-card" :color="emphasis" large />
    </Title>
</div>

<div class="block">
    <Card :classes="classes" shadow>
        <template #toolbar>
            <Button label="Toolbar" color="#bbbbbb" subtle uppercase sm />
        </template>
        <template #toolbar-right>
            <Badge content="toolbar-right" uppercase />
        </template>
        <template #header>
            <Title h4 title="Header (using co-title)" overline="overline" :classes="classes">
                <template #subtitle>Subtitle - <LoremIpsum add="5-10w" /></template>
            </Title>
        </template>
        <template #header-right>
            <Badge content="header-right" uppercase />
        </template>
        <template #before>
            <Badge content="before-content" :color="emphasis" uppercase /> <LoremIpsum add="5w" />
        </template>
        <template #content>
            <LoremIpsum add="2s" />
        </template>
        <template #actions>
            <Button label="actions" :color="emphasis" outline uppercase />
        </template>
        <template #actions-right>
            <Button label="actions-right" :color="emphasis" text-color="#ffffff" filled uppercase />
        </template>
    </Card>
</div>

<div class="block">
    <Card :classes="classes" shadow>
        <template #header>
            <Title h5 title="My Second Card" :classes="classes">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </Title>
        </template>
        <template #header-right>
            <Button label="&times;" color="#cccccc" light />
        </template>
        <template #before-content>
            <Button label="&times;" color="#cccccc" light />
        </template>
    </Card>

    <Card :classes="classes" shadow>
        <template #header>
            <Title h5 title="My Third Card" :classes="classes">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </Title>
        </template>
        <template #actions>
            <Button label="button" :color="emphasis" text-color="#ffffff" filled />
        </template>
    </Card>
</div>
<div class="block space-below">
    <Card :classes="{ before: 'co-bg-lightgrey block-center' }" no-spacer>
        <template #before>
            <div class="flex co-center">Empty Card using <Badge content="before" />slot and <Badge content="no-spacer" color="#bbbbbb" /> prop.</div>
        </template>
    </Card>
</div>

<TextBlock>

<Title h6 title="Slots" overline="co-card" subtitle="each slot is optional. The card will add space only for the needed slots." side :classes="classes" />

<div class="block">
    <div class="width-125">
        <Badge content="toolbar" /><Badge content="toolbar-right" />
    </div>
    <div class="flex">
        Are within the upper padding. Generally used for buttons, labels, etc.
    </div>
</div>


<div class="block">
    <div class="width-125">
        <Badge content="header" /><Badge content="header-right" />
    </div>
    <div class="flex">
        Make up the main title block.
    </div>
</div>


<div class="block">
    <div class="width-125">
        <Badge content="before" />
    </div>
    <div class="flex">
        Is a special section without padding: useful for alerts/warnings. Use in conjunction with <Badge content="no-spacer" color="#bbbbbb" /> to create an 'empty' card.
    </div>
</div>

<div class="block">
    <div class="width-125">
        <Badge content="content" />
    </div>
    <div class="flex">
        is the main content block, with padding.
    </div>
</div>

<div class="block">
    <div class="width-125">
        <Badge content="actions" />
        <Badge content="actions-right" />
    </div>
    <div class="flex">
        contain the buttons/actions for the card, within the lower padding.
    </div>
</div>

<Title h6 title="Props" overline="co-card" subtitle="Each prop is optional. By default, they are all disabled." side :classes="classes" />

<div class="block">
    <div class="width-125">
        <Badge content="no-margin" />
        <Badge content="boolean" color="#bbbbbb" />
    </div>
    <div class="flex">
        removes the default margin surrounding each card.
    </div>
</div>
<div class="block">
    <div class="width-125">
        <Badge content="no-spacer" />
        <Badge content="boolean" color="#bbbbbb" />
    </div>
    <div class="flex">
        removes the extra padding from the top/bottom border radius.
    </div>
</div>
<div class="block">
    <div class="width-125">
        <Badge content="shadow" />
        <Badge content="boolean" color="#bbbbbb" />
    </div>
    <div class="flex">
        adds a subtle drop shadow.
    </div>
</div>
<div class="block">
    <div class="width-125">
        <Badge content="dense" />
        <Badge content="boolean" color="#bbbbbb" />
    </div>
    <div class="flex">
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

        const emphasis = '#ff69b4'

        const classes = {
            card: 'co-bg',
            before: 'co-padding co-bg-lightemphasis',
            overline: 'co-text-emphasis',
            subtitle: 'co-text-tint-2',
            actions: 'co-bg-lightgrey',
            content: 'co-text-tint-1',
        }

        return {
            emphasis,
            classes
        }
    }

})

</script>
<style lang="scss" scoped>
.block {
    margin: 1em 0;
}
</style>