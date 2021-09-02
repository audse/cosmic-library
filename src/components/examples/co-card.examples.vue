<template>

<div class="space-below">
    <Title h4 subtitle="Cards are a general-purpose container for content.">
        <Badge content="co-card" large />
    </Title>
</div>

<div class="narrow block space-below">
    <Card :classes="classes" shadow>
        <template #toolbar-right>
            <Badge content="new card" uppercase />
        </template>
        <template #header>
            <Title h4 title="My First Card" overline="Sep 1, 2021" :classes="classes">
                <template #subtitle><LoremIpsum add="5-10w" /></template>
            </Title>
        </template>
        <template #content>
            <LoremIpsum add="2s" />
        </template>
        <template #actions>
            <Button label="save" color="grey" subtle uppercase lg />
        </template>
    </Card>
</div>

</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import Badge from './../co-badge'
import Button from './../co-button'
import Title from './../co-title'
import Card from './../co-card'

export default defineComponent({
    
    name: 'CoCardExamples',

    components: {
        LoremIpsum,
        Title,
        Card,
        Badge,
        Button,
    },

    setup () {

        const classes = {
            overline: 'text-pink',
            actions: 'bg-lightgrey'
        }

        return {
            classes
        }
    }

})

</script>
