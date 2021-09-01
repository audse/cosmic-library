<template>

<CoCard v-for="card in my_cards" :key="card.title" v-bind="card" :classes="classes">
    <template #content>
        {{ card.content }}
    </template>
</CoCard>

</template>

<script>

import { defineComponent, ref } from 'vue'

import CoCard from './../components/CoCard'

export default defineComponent({
    
    name: 'HomePage',

    components: {
        CoCard,
    },

    setup () {

        const date = ref('Sep 1, 2021')

        const classes = {
            overline: 'pink',
        }

        const my_cards = [
            {
                title: 'My First Card',
                subtitle: 'Isn\'t this a great card?',
                overline: 'Sep 1, 2021',
                content: 'This is some more information about this card.'
            },
            {
                title: 'My Second Card',
                subtitle: 'Some more information.',
                overline: 'Sep 2, 2021',
                content: 'This is another example with some more information.'
            },

        ]

        return {
            date,
            my_cards,
            classes,
        }
    }

})

</script>
