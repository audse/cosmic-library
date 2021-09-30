<template>
    
<ul :class="[rippleDark||rippleLight||rippleColor ? 'ripple' : '', classList.list]">
    <slot></slot>
</ul>

</template>

<script>
import { defineComponent, reactive, computed } from 'vue'

export default defineComponent({

    name: 'co-list',

    props: {
        classes: Object,

        borderColor: String,

        hoverDark: Boolean,
        hoverLight: Boolean,
        hoverColor: String,

        rippleDark: Boolean,
        rippleLight: Boolean,
        rippleColor: Boolean,
    },

    setup ( props ) {
        
        const classList = reactive( props.classes ? props.classes : {} )

        const hoverBg = computed( () => (props.rippleColor || props.rippleDark || props.rippleLight) ? '' : props.hoverColor ? props.hoverColor : props.hoverDark ? 'rgba(0,0,0,0.1)' : props.hoverLight ? 'rgba(255,255,255,0.1)' : '' )
        const rippleBg = computed( () => props.rippleColor ? props.rippleColor : props.rippleDark ? 'rgba(0,0,0,0.2)' : props.rippleLight ? 'rgba(255,255,255,0.2)' : '' )

        return {
            classList,

            hoverBg,
            rippleBg,
        }

    },
})
</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
    display: block;
    position: relative;
    margin: 0;
    padding: 0;

    &:focus {
        outline: none;
    }
}

ul::v-deep li {

    background: rgba(0,0,0,0);

    display: flex;
    border-bottom: 1px solid v-bind(borderColor);
    align-items: center;

    &:last-of-type {
        border-bottom: none;
    }

    &:hover {
        background: v-bind(hoverBg);
        transition: 100ms;
    }

    &:focus-visible {
        outline: initial;
    }

    section {
        flex: 1 auto;
    }

    aside.left {
        padding: 0.5em;
        text-align: left;
        justify-self: start;
        flex: none;
    }

    aside.right {
        padding: 0.5em;
        text-align: right;
        justify-content: right;
        justify-self: end;
        flex: none;
    }

    section.content {
        padding: 1em 0.5em;
    }
}

ul.ripple::v-deep li {
    background-position: center;
    transition: background 800ms;
    -webkit-transition: background 800ms;
    z-index: 1;
    
    &:hover {
        background: v-bind(rippleBg) radial-gradient(circle, transparent 1%, v-bind(rippleBg) 1%) center/15000%;
    }

    &:active {
        background-color: v-bind(rippleBg);
        background-size: 100%;
        transition: background 0s;
    }
}


</style>
