<template>

<figure :class="classList.avatar">
    <figcaption :class="classList.content">
        <slot></slot>
    </figcaption>
</figure>

</template>

<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'co-avatar',
    
    props: {

        classes: Object,

        bg: String,
        textColor: String,

        xs: Boolean,
        sm: Boolean,
        lg: Boolean,
        xl: Boolean,
    },

    setup ( props ) {

        const classList = reactive( props.classes ? props.classes : {} )

        const size = computed( () => props.xs ? '1em' : props.sm ? '1.75em' : props.lg ? '3.25em' : props.xl ? '4em' : '2.5em' )

        return {
            classList,
            size
        }
        
    },
})
</script>

<style lang="scss" scoped>

* {
    /* Box Model */
    box-sizing: border-box;
    display: inline-block;
    margin: 0;
    padding: 0;

    /* Positioning */
    position: relative;
}

figure {
    /* Circle Style */
    clip-path: circle( calc( v-bind(size) / 2 ) at 50% 50% );

    /* Box Style */
    background: v-bind(bg);
    border-radius: v-bind(size);
    color: v-bind(textColor);

    /* Sizing */
    width: v-bind(size);
    height: v-bind(size);
}

figcaption {
    /* Positioning */
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

</style>