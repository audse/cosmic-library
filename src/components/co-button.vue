<template>
    
    <button :class="class_list" :type="type ? type : 'submit'" :style="style">
        {{ label }}
        <slot></slot>
        <transition enter-active-class="ripple">
            <span></span>
        </transition>
    </button>   

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

        uppercase: Boolean,

        filled: Boolean,
        outline: Boolean,
        subtle: Boolean,

        sm: Boolean,
        lg: Boolean,
    },

    setup ( props ) {

        const class_list = computed( () => {
            let string = 'co-button'

            if ( props.classes ) string += ` ${props.classes}`

            if ( props.uppercase ) string += ' co-button-uppercase'

            if ( props.sm ) string += ' co-button-sm'
            if ( props.lg ) string += ' co-button-lg'

            return string
        })

        const style = {
            color: props.subtle || props.outline ? props.color : 'inherit',
            background: props.filled ? props.color : 'none',
            border: props.outline ? `2px solid ${props.color}` : 'none'
        }

        return {
            class_list,
            style
        }

    }

})

</script>

<style scoped>

button {
    border: 0;
    outline: 0;
    background: unset;
    color: unset;
    text-transform: unset;
    font-weight: unset;
    letter-spacing: unset;
    font-size: unset;
}

.co-button {

    /* Background */
    border-radius: 1em;

    /* Text */
    letter-spacing: 1px;
    font-weight: 600;
    font-size: 0.9rem;

    /* Positioning */
    display: inline-block;

    /* Spacing */
    margin: 0.25em 0.5em 0.25em 0;
    padding: 0.25em 0.5em 0.15em 0.5em;

    /* Sizing */
    width: fit-content;
}

.co-button-sm {
    font-size: 0.75rem;
    padding: 0.1em 0.3em;
    border-width: 1px;
}

.co-button-lg {
    font-size: 1rem;
    padding: 0.5em 0.75em;
}

.co-button-uppercase {
    text-transform: uppercase;
}

span.ripple {
    position: absolute; /* The absolute position we mentioned earlier */
    border-radius: 50%;
    transform: scale(0);
    animation: ripple 600ms linear;
    background-color: rgba(255, 255, 255, 0.7);
}

@keyframes ripple {
    to {
        transform: scale(4);
        opacity: 0;
    }
}

</style>
