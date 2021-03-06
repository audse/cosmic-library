<template>
    
<button :class="['button', classList.container]">
    <label :class="classList.button" :type="type ? type : 'submit'">
        <span>
        {{ label }}
        <slot></slot>
        </span>
    </label>   
</button>

</template>
<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'co-button',

    props: {
        type: String,
        label: String,
        classes: String,

        color: String,
        labelColor: String,

        uppercase: Boolean,

        filled: Boolean,
        outline: Boolean,
        subtle: Boolean,
        light: Boolean,

        round: Boolean,

        sm: Boolean,
        lg: Boolean,
    },

    setup ( props ) {

        const classList = reactive({

            button: computed( () => {
                let string = ''

                if ( props.classes && props.classes.button ) string += ` ${props.classes.button}`

                if ( props.uppercase ) string += ' uppercase'

                if ( props.filled ) string += ' filled ripple-filled'
                if ( props.subtle ) string += ' subtle ripple-subtle'
                if ( props.light ) string += ' light ripple-light'
                if ( props.outline ) string += ' outline ripple-outline'

                if ( props.round ) string += props.sm ? ' round-sm' : props.lg ? ' round-lg' : ' round'

                if ( props.sm ) string += ' sm'
                if ( props.lg ) string += ' lg'

                return string
            })
        })

       
        
        const changeOpacity = (color, opacity) => {
            const newOpacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + newOpacity.toString(16).toUpperCase();
        }

        const colorOpacity25 = computed( () => props.color ? changeOpacity(props.color, 0.25) : 'rgba(0, 0, 0, 0.15)' )
        const colorOpacity50 = computed( () => props.color ? changeOpacity(props.color, 0.50) : 'rgba(0, 0, 0, 0.15)' )

        const textColor = props.labelColor ? props.labelColor : props.subtle || props.outline ? props.color : 'inherit'
        const backgroundColor = props.filled ? props.color : props.light ? colorOpacity25.value : 'transparent'
        const border = props.outline ? `2px solid ${colorOpacity50.value}` : 'none'

        return {
            classList,
            textColor,
            backgroundColor,
            colorOpacity25,
            colorOpacity50,
            border,
        }

    }

})

</script>

<style lang="scss" scoped>

* {
    display: inline-block;
    box-sizing: border-box;
    position: relative;
    padding: 0;
    margin: 0;
}

.button {
    /* Reset */
    border: 0;
    outline: 0;
    background: unset;
    color: unset;
    text-transform: unset;
    font-weight: unset;
    letter-spacing: unset;
    font-size: unset;
    font-family: unset;
    word-wrap: normal;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    
    /* Background */
    border-radius: 1.5em;

    /* Positioning */
    display: inline-block;
    position: relative;
    isolation: isolate;

    /* Spacing */
    margin: 0.25em 0.5em 0.25em 0;

    /* Sizing */
    width:  fit-content;
    min-width: fit-content;

    &:hover {
        transform: translate(0, -1px);
        opacity: 0.9;
        transition: 200ms;
        -webkit-transition: 200ms;
        z-index: 1;
    }

    /* Allow outline when focusing using tab (for accessibility) */
    &:focus-visible {
        outline: auto;
    }

    label {

        /* Styles */
        border: v-bind(border);
        background: v-bind(backgroundColor);
        color: v-bind(textColor);

        /* Box Model */
        border-radius: 1.5em;
        display: flex;
        align-items: center;

        /* Spacing */
        padding: 0.55em 1.25em;

        /* Sizing */
        min-width: 44px;
        min-height: 44px;
        

        span {
            display: block;

            /* Text */
            letter-spacing: 0.5px;
            font-weight: 600;
            font-size: 0.8rem;
            
        }
    }
}

.round, .round-sm, .round-lg {

    min-width: 0;
    min-height: 0;

    span {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%)
    }
}

.round {
    width: 2.5em;
    height: 2.5em;
}

.round-sm {
    width: 2em;
    height: 2em;
}

.round-lg {
    width: 3em;
    height: 3em;
    border-radius: 1.5em;
}

.sm {
    font-size: 0.75rem;
    padding: 0.4em 0.75em;
    border-width: 1px;
}

.lg {
    font-size: 0.9rem;
    padding: 0.5em 1.5em;
}

.uppercase {
    text-transform: uppercase;
}

.ripple-filled, .ripple-subtle, .ripple-light, .ripple-outline {
    background-position: center;
    background-blend-mode: screen;
    transition: background 800ms;
    -webkit-transition: background 800ms;
    z-index: 1;
}

.ripple-filled:hover {
    background: v-bind(backgroundColor) radial-gradient(circle, transparent 1%, v-bind(backgroundColor) 1%) center/15000%;
}

.ripple-subtle:hover, .ripple-outline:hover {
    background: v-bind(colorOpacity25) radial-gradient(circle, transparent 1%, v-bind(colorOpacity25) 1%) center/15000%;
}

.ripple-light:hover {
    background: v-bind(colorOpacity50) radial-gradient(circle, transparent 1%, v-bind(colorOpacity50) 1%) center/15000%;
}

.ripple-filled:active, .ripple-subtle:active, .ripple-outline:active, .ripple-light:active {
    background-color: v-bind(backgroundColor);
    background-size: 100%;
    transition: background 0s;
    -webkit-transition: background 0s;
}


</style>
