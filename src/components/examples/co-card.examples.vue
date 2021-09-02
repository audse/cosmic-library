<template>

<div class="space-below">
    <Title h3 subtitle="co-cards are a general-purpose container for content." :classes="classes">
        <Badge left="<" content="co-card" right=" />" :color="emphasis" />
        co-card <span class="co-text-tint-1">component</span>
    </Title>
</div>

<div class="block">
    <Card :classes="classes" shadow-dark>
        <LoremIpsum add="2s" />
        <template #toolbar>
            <Badge content="Toolbar" :color="grey" subtle uppercase sm />
        </template>
        <template #toolbar-right>
            <Badge content="toolbar-right" :color="white" uppercase sm />
        </template>
        <template #header>
            <Title h4 overline="overline" :classes="classes">
                Header (using co-title)
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
    <Card :classes="classes" shadow-dark margin-lg>
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

    <Card :classes="{ card: 'co-bg', card: 'co-bg-mixemphasis'}" shadow-dark margin-lg>
        <template #header>
            <Title h5 title="My Third Card" :classes="{title: 'co-text-truewhite', subtitle: 'co-text-emphasis-text'}">
                <template #subtitle><LoremIpsum add="4-8w" /></template>
            </Title>
            <Badge content="incomplete" :color="truewhite" subtle sm />
            <Badge content="new" :color="emphasis_light" subtle sm />
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
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><Title title="Option A" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option A" :color="white" subtle />
        </template>
    </Card>
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><Title title="Option B" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option B" :color="emphasis" outline />
        </template>
    </Card>
    <Card :classes="{ card: 'co-bg-lightgrey co-center-text', content: 'co-text-tint-2' }" shadow-dark margin-sm>
        <template #header><Title title="Option C" /></template>
        <LoremIpsum add="10w" />
        <template #actions>
            <Button label="Option C" :color="emphasis" filled :text-color="truewhite" />
        </template>
    </Card>
</div>


<TextBlock class="co-text-tint-1">

<Title h5 title="Slots" overline="co-card" subtitle="each slot is optional. The card will add space only for the needed slots." side :classes="classes" />

<div class="block space-above">
    <Badge left="#" content="default" />
</div>


<div class="block space-above">
    <Badge left="#" content="toolbar" :color="white" /><Badge left="#" content="toolbar-right" :color="white" />
</div>


<div class="block space-above">
    <Badge left="#" content="header" :color="white" /><Badge left="#" content="header-right" :color="white" />
</div>


<div class="block space-above">
    <Badge left="#" content="before" :color="white" />

    Use in conjunction with <Badge content="no-spacer" :color="grey" sm /> to create an 'empty' card.
</div>


<div class="block space-above">
    <Badge left="#" content="actions" :color="white" />
    <Badge left="#" content="actions-right" :color="white" />
</div>

<div class="space-below" />

<Title h5 title="Props" overline="co-card" subtitle="Each prop is optional. By default, they are all disabled." side :classes="classes" />

<div class="block space-above">
    <Badge content="boolean" :color="emphasis" />
    <Badge content="no-margin" :color="white" />
    <Badge content="margin-sm" :color="white" />
    <Badge content="margin-lg" :color="white" />
</div>


<div class="block space-above">
    <Badge content="boolean" :color="emphasis" />
    <Badge content="no-spacer" :color="white" />
</div>


<div class="block space-above">
    <Badge content="boolean" :color="emphasis" />
    <Badge content="shadow" :color="white" />
    <Badge content="shadow-light" :color="white" />
    <Badge content="shadow-dark" :color="white" />

    choose <Badge content="shadow-light" :color="grey" sm /> for light backgrounds, or <Badge content="shadow-dark" :color="grey" sm /> for dark backgrounds.
</div>


<div class="block space-above">
    <Badge content="boolean" :color="emphasis" />
    <Badge content="dense" :color="white" />
</div>

<div class="space-above" />

<Title h5 title="Class Object" overline="co-card" :classes="classes" />

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
            classes
        }
    }

})

</script>
<style lang="scss" scoped>

.space-above {
    padding-top: 1.5em;
}

.block {
    margin: 0.5em 0;
    display: flex;
    align-items: center;
}

</style>