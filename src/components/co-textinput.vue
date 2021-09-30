<template>

<section :class="[classList.group, focused ? 'focused' : '', hasText, !noShadow ? 'shadow' : '' ]">

    <!-- Transition Label On Focus -->
    <label
    :id="`text-input-label-${label}`"
    :for="`text-input-${label}`"
    :class="[classList.label, bg ? 'filled' : '', material ? 'material' : '' ]">
        {{ label }}
        <slot name="label"></slot>
    </label>

    <input
    :id="`text-input-${label}`" 
    :aria-label="`text-input-${label}`"
    :placeholder="placeholder"
    type="text"
    :class="[outlineColor && !material ? 'outline' : '', bg ? 'filled' : '', material ? 'material' : '']"
    @focus="focused=true"
    @blur="focused=false"
    @input="this.$emit('update:modelValue', $event.target.value)"
    tabindex="0" />

</section>

</template>
<script>

import { computed, defineComponent, reactive, ref, toRefs, watch } from 'vue'

export default defineComponent({

    name: 'co-text-input',

    props: {
        modelValue: String,

        label: String,
        placeholder: String,

        bg: String,
        placeholderColor: String,
        outlineColor: String,
        textColor: String,

        width: String,
        
        material: Boolean,

        noShadow: Boolean,
    },

    emits: ['update:modelValue'],

    setup ( props ) {

        const classList = reactive( props.classes ? props.classes : {} )

        const focused = ref(false)

        const modelValueRef = toRefs(props).modelValue

        const hasText = ref('')
        watch(modelValueRef, () => {
            if ( modelValueRef.value.length > 0 ) hasText.value = 'hasText'
            else hasText.value = ''
        })

        const sectionWidth = ref( props.width ? props.width : 'fit-content')

        const labelWidth = computed( () => {
            const labelElement = document.getElementById(`text-input-label-${props.label}`)
            return `${Math.floor(labelElement.getBoundingClientRect().width)}px`
        })

        const changeOpacity = (color, opacity) => {
            const newOpacity = Math.round(Math.min(Math.max(opacity || 1, 0), 1) * 255);
            return color + newOpacity.toString(16).toUpperCase();
        }

        const backgroundColor = computed( () => {
            if ( props.bg && props.subtle ) {
                return changeOpacity(props.bg, 0.25)
            } else if ( props.bg ) return props.bg
            else return 'transparent'
        })

        const labelColor = !props.outlineColor && props.textColor ? props.textColor : props.outlineColor ? props.outlineColor : 'inherit'

        const borderColor = changeOpacity(labelColor, 0.5)
        const placeholderTextColor = changeOpacity( props.placeholderColor ? props.placeholderColor : props.textColor ? props.textColor : labelColor, 0.5)
        const materialBorderColor = changeOpacity( props.textColor ? props.textColor : labelColor, 0.15)
        const inputColor = props.textColor ? props.textColor : 'inherit'

        return {
            classList,
            focused,
            hasText,
            sectionWidth,
            labelWidth,
            backgroundColor,
            labelColor,
            borderColor,
            placeholderTextColor,
            materialBorderColor,
            inputColor
        }

    },
})

</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
    display: block;
    margin: 0;
    padding: 0;
    background: none;
    border: none;
    outline: none;
    position: relative;
    font-size: 1em;
}

section {
    isolation: isolate;
    display: inline-block;
    margin-top: 0.5em;
    padding-top: 0.5em;
    width: v-bind(sectionWidth);

    input::placeholder {
        opacity: 0;
    }

    &.hasText {

        transition: all 200ms;
        
        label {
            top: 0;
            transform: scale(85%);
            transform-origin: bottom left;
            transition: all 200ms;
            opacity: 0.75;
        }

        label.filled, label.material {
            top: 0.6em;
        }

        label.material {
            color: v-bind(labelColor)
        }

        input::placeholder {
            opacity: 1;
            transition: opacity 200ms;
        }

        input.outline {
            /* Remove part of border when label hovers */
            clip-path: polygon(1.25em 2px, calc( v-bind(labelWidth) + 1.75em ) 2px, calc( v-bind(labelWidth) + 1.75em ) 0, 100% 0, 100% 100%, 0 100%, 0 0, 1.25em 0);
            transition: all 200ms;
        }

        input.material {
            border-bottom-color: v-bind(materialBorderColor);
        }

    }
}

label {
    position: absolute;
    top: calc( 50% - 0.5em );
    left: 0.75em;
    transform: scale(100%);
    transition: all 200ms;
    z-index: 2;
    width: fit-content;
    max-width: 100%;

    color: v-bind(labelColor);
}

label.material {
    color: v-bind(placeholderTextColor);
    left: 0.25em;
}

input {
    padding: 1.5em 0.75em 0.5em 0.75em;
    z-index: 1;
    color: v-bind(inputColor);
    background-color: v-bind(backgroundColor);
    width: 100%;

    &::placeholder {
        color: v-bind(placeholderTextColor);
    }

    &:focus-visible {
        outline: initial;
    }
}

input.shadow {
    box-shadow: 0px 0px 0px 0px rgba(0, 0, 0, 0);
}

input.outline {

    /* Remove part of border-top when label hovers */
    -webkit-clip-path: polygon(1.25em 0, calc( v-bind(labelWidth) + 1.75em ) 0, calc( v-bind(labelWidth) + 1.75em ) 0, 100% 0, 100% 100%, 0 100%, 0 0, 1.25em 0);
    clip-path: polygon(1.25em 0, calc( v-bind(labelWidth) + 1.75em ) 0, calc( v-bind(labelWidth) + 1.75em ) 0, 100% 0, 100% 100%, 0 100%, 0 0, 1.25em 0);
    transition: all 200ms;

    border: 2.5px solid v-bind(borderColor);
    border-radius: 0.75em;
}

input.material {
    padding-left: 0.25em;
    padding-right: 0.25em;
    transition: all 200ms;
    border-bottom: 2.5px solid v-bind(materialBorderColor);
}

input.filled {
    border-radius: 0.75em;
}

/* On Focus */
section.focused {

    &.shadow {
        box-shadow: 0px 10px 15px -5px rgba(0, 0, 0, 0.15);
    }

    transition: all 200ms;
    
    label {
        top: 0;
        transform: scale(85%);
        transform-origin: bottom left;
        transition: all 200ms;
        opacity: 0.75;
    }

    label.filled, label.material {
        top: 0.6em;
    }

    label.material {
        color: v-bind(labelColor)
    }

    input::placeholder {
        opacity: 1;
        transition: opacity 200ms;
    }

    input.outline {
        /* Remove part of border when label hovers */
        -webkit-clip-path: polygon(0em 2px, calc( v-bind(labelWidth) + 0.75em ) 2px, calc( v-bind(labelWidth) + 0.75em ) 0, 100% 0, 100% 100%, 0 100%, 0 0, 1.25em 0);
        clip-path: polygon(0em 2px, calc( v-bind(labelWidth) + 0.75em ) 2px, calc( v-bind(labelWidth) + 0.75em ) 0, 100% 0, 100% 100%, 0 100%, 0 0, 1.25em 0);
        transition: all 200ms;
    }

    input.material {
        border-bottom-color: v-bind(borderColor);
    }
}



</style>
