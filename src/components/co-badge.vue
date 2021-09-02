<template>
    
<div :style="style" :class="['co-badge', uppercase ? 'co-badge-uppercase' : '', lg ? 'co-badge-size-lg' : sm ? 'co-badge-size-sm' : 'co-badge-size-md']">

    <span class="co-badge-aside">
        {{ left }}
        <slot name="left"></slot>
    </span>

    {{ content }}
    <slot></slot>

    <span class="co-badge-aside">
        {{ right }}
        <slot name="right"></slot>
    </span>
</div>

</template>
<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'co-badge',

    props: {
        content: String,

        left: String,
        right: String,

        color: String,

        lg: Boolean,
        sm: Boolean,

        uppercase: Boolean,
    },

    setup ( props ) {

        const change_alpha = (color, opacity) => {
            const new_opacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + new_opacity.toString(16).toUpperCase();
        }

        const new_color = computed( () => props.color ? change_alpha(props.color, 0.25) : 'rgba(0, 0, 0, 0.15)' )

        const style = reactive({
            color: props.color,
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
    margin: 0.15em 0.25em;
    padding: 0.2em 0.75em;

    /* Sizing */
    width: fit-content;
    height: fit-content;
}

.co-badge-aside {
    opacity: 0.5;
}

.co-badge-size-lg {
    font-size: 1em;
}

.co-badge-size-md {
    font-size: 0.75em;
}

.co-badge-size-sm {
    font-size: 0.6em;
}

.co-badge-uppercase {
    text-transform: uppercase;
}

</style>
