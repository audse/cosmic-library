<template>
    
<span :class="[classList.badge, uppercase ? 'uppercase' : '', lg ? 'lg' : sm ? 'sm' : 'md', noWrap ? 'no-wrap' : '']">

    <aside v-if="this.$slots.left" :class="classList.left">
        {{ left }}
        <slot name="left"></slot>
    </aside>

    {{ content }}
    <slot></slot>

    <aside v-if="this.$slots.right" :class="classList.right">
        {{ right }}
        <slot name="right"></slot>
    </aside>
</span>

</template>
<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'co-badge',

    props: {
        content: String,

        classes: Object,

        noWrap: Boolean,

        filled: Boolean,
        subtle: Boolean,
        color: String,
        labelColor: String,

        lg: Boolean,
        sm: Boolean,

        uppercase: Boolean,
    },

    setup ( props ) {

        const classList = reactive( props.classes ? props.classes : {} )

        const changeOpacity = (color, opacity) => {
            const newOpacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + newOpacity.toString(16).toUpperCase();
        }

        const backgroundColor = computed( () => props.subtle ? 'transparent' : props.filled && props.labelColor ? props.color : props.color ? changeOpacity(props.color, 0.25) : 'rgba(0, 0, 0, 0.15)' )

        const textColor = computed( () => props.labelColor ? props.labelColor : props.color )

        return {
            classList,
            backgroundColor,
            textColor
        }
    }

})

</script>

<style scoped>

* {
    box-sizing: border-box;
    display: inline-block;
}

span {

    /* Background */
    border-radius: 1em;
    background-color: v-bind(backgroundColor);
    color: v-bind(textColor);

    /* Text */
    letter-spacing: 0.5px;

    /* Spacing */
    margin: 0.15em 0.25em;
    padding: 0.2em 0.75em;

    /* Sizing */
    height: fit-content;
    max-height: fit-content;
}

aside {
    opacity: 0.5;
}

.no-wrap {
    width: fit-content;
    min-width: max-content;
}

.lg {
    font-size: 1em;
}

.md {
    font-size: 0.75em;
}

.sm {
    font-size: 0.6em;
}

.uppercase {
    text-transform: uppercase;
}

</style>
