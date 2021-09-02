<template>
    
    <div class="co-button-container">
    <button :class="class_list" :type="type ? type : 'submit'">
        <div class="co-button-label">
        {{ label }}
        <slot></slot>
        </div>
    </button>   
    </div>

</template>
<script>

import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'CoButton',

    props: {
        type: String,
        label: String,
        classes: String,

        color: String,
        textColor: String,

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

        const class_list = computed( () => {
            let string = 'co-button'

            if ( props.classes ) string += ` ${props.classes}`

            if ( props.uppercase ) string += ' co-button-uppercase'

            if ( props.filled ) string += ' co-button-filled co-button-ripple-filled'
            if ( props.subtle ) string += ' co-button-subtle co-button-ripple-subtle'
            if ( props.light ) string += ' co-button-light co-button-ripple-light'
            if ( props.outline ) string += ' co-button-outline co-button-ripple-outline'

            if ( props.round ) string += props.sm ? ' co-button-round-sm' : props.lg ? ' co-button-round-lg' : ' co-button-round'

            if ( props.sm ) string += ' co-button-sm'
            if ( props.lg ) string += ' co-button-lg'

            return string
        })
        
        const change_alpha = (color, opacity) => {
            const new_opacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + new_opacity.toString(16).toUpperCase();
        }

        const color_25 = computed( () => props.color ? change_alpha(props.color, 0.25) : 'rgba(0, 0, 0, 0.15)' )
        const color_50 = computed( () => props.color ? change_alpha(props.color, 0.50) : 'rgba(0, 0, 0, 0.15)' )

        const text_color = props.textColor ? props.textColor : props.subtle || props.outline ? props.color : 'inherit'
        const background_color = props.filled ? props.color : props.light ? color_25.value : 'transparent'
        const border = props.outline ? `2px solid ${color_50.value}` : 'none'

        return {
            class_list,
            text_color,
            background_color,
            color_25,
            color_50,
            border,
        }

    }

})

</script>

<style lang="scss" scoped>

button,
.co-button-container,
.co-button {
    box-sizing: border-box;
}

button {
    border: 0;
    outline: 0;
    background: unset;
    color: unset;
    text-transform: unset;
    font-weight: unset;
    letter-spacing: unset;
    font-size: unset;
    font-family: unset;
}

.co-button-container {
    
    /* Background */
    border-radius: 1.25em;

    /* Positioning */
    display: inline-block;
    position: relative;

    /* Spacing */
    margin: 0.25em 0.5em 0.25em 0;

    /* Sizing */
    width:  fit-content;
}

.co-button {

    /* Styles */
    border: v-bind(border);
    background-color: v-bind(background_color);
    color: v-bind(text_color);

    /* Background */
    border-radius: 1.25em;

    /* Text */
    letter-spacing: 0.5px;
    font-weight: 600;
    font-size: 0.8rem;

    /* Positioning */
    position: relative;

    /* Spacing */
    padding: 0.55em 0.9em;

    /* Sizing */
    width: fit-content;
}

.co-button-container:hover {
    opacity: 0.9;
    transition: 200ms;
}

.co-button-round, .co-button-round-sm, .co-button-round-lg {

    .co-button-label {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%)
    }
}

.co-button-round {
    width: 2.25em;
    height: 2.25em;
}

.co-button-round-sm {
    width: 1.75em;
    height: 1.75em;
}

.co-button-round-lg {
    width: 3em;
    height: 3em;
    border-radius: 1.5em;
}

.co-button-sm {
    font-size: 0.75rem;
    padding: 0.4em 0.75em;
    border-width: 1px;
}

.co-button-lg {
    font-size: 1rem;
    padding: 0.5em 0.75em;
}

.co-button-uppercase {
    text-transform: uppercase;
}

.co-button-ripple-filled, .co-button-ripple-subtle, .co-button-ripple-light, .co-button-ripple-outline {
    background-position: center;
    transition: background 800ms;
}

.co-button-ripple-filled:hover {
    background: v-bind(background_color) radial-gradient(circle, transparent 1%, v-bind(background_color) 1%) center/15000%;
    background-blend-mode: screen;
}

.co-button-ripple-filled:active {
    background-color: v-bind(background_color);
    background-size: 100%;
    transition: background 0s;
}

.co-button-ripple-subtle:hover, .co-button-ripple-outline:hover {
    background: v-bind(color_25) radial-gradient(circle, transparent 1%, v-bind(color_25) 1%) center/15000%;
    background-blend-mode: screen;
}

.co-button-ripple-subtle:active, .co-button-ripple-outline:active {
    background-color: v-bind(background_color);
    background-size: 100%;
    transition: background 0s;
}

.co-button-ripple-light:hover {
    background: v-bind(color_50) radial-gradient(circle, transparent 1%, v-bind(color_50) 1%) center/15000%;
    background-blend-mode: screen;
}

.co-button-ripple-light:active {
    background-color: v-bind(background_color);
    background-size: 100%;
    transition: background 0s;
}


</style>
