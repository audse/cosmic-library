<template>
    
<div :style="style" :class="['co-badge', classes, uppercase ? 'co-badge-uppercase' : '', lg ? 'co-badge-size-lg' : 'co-badge-size-md']">
    {{ content }}
    <slot></slot>
</div>

</template>
<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'CoBadge',

    props: {
        content: String,
        classes: String,

        color: String,

        lg: Boolean,
        uppercase: Boolean,
    },

    setup ( props ) {

        const change_alpha = (color, opacity) => {
            const new_opacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + new_opacity.toString(16).toUpperCase();
        }

        const new_color = computed( () => props.color ? change_alpha(props.color, 0.25) : 'rgba(0, 0, 0, 0.15)' )

        const style = reactive({
            background: new_color.value
        })

        return {
            style
        }
    }

})

</script>

<style scoped>

.co-badge {

    /* Background */
    border-radius: 1em;

    /* Text */
    letter-spacing: 0.5px;

    /* Positioning */
    display: inline-block;

    /* Spacing */
    margin: 0 0.5em;
    padding: 0.25em 0.5em 0.1em 0.5em;

    /* Sizing */
    width: fit-content;
}

.co-badge-size-lg {
    font-size: 1em;
}

.co-badge-size-md {
    font-size: 0.75em;
}

.co-badge-uppercase {
    text-transform: uppercase;
}

</style>
