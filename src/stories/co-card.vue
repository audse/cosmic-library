<template>
    

</template>
<script>
import { computed, reactive } from 'vue'

export default {

    name: 'co-card',

    props: {

        bg: {
            type: String,
            required: false,
        },

        shadow: {
            type: String,
            validator: function (value) {
                return ['light', 'medium', 'dark'].indexOf(value) !== -1;
            },
        },

        dense: Boolean,

        lessRound: Boolean,
        noSpacer: Boolean,

    },

    setup ( props ) {

        props = reactive(props)
        
        const classes = computed( () => ({
            card: {
                'cosmic-card': true,
                [`cosmic-shadow--${props.shadow || 'medium'}`]: props.shadow
            }
        }))

    },
}
</script>
