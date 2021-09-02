<template>

<div :class="['co-title', class_list.title_group]" :style="{ fontSize: font_size }">
    <div :class="['co-title-title', class_list.title]">

        <div :class="['co-title-overline', class_list.overline]">
            {{ overline }}
            <slot name="overline"></slot>
        </div>

        {{ title }}

        <slot></slot>
    </div>
    <div :class="['co-title-subtitle', class_list.subtitle]">
        {{ subtitle }}
        <slot name="subtitle"></slot>
    </div>
</div>

</template>
<script>
import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'CoTitle',

    props: {
        title: String,
        subtitle: String,
        overline: String,

        classes: Object,

        h1: Boolean,
        h2: Boolean,
        h3: Boolean,
        h4: Boolean,
        h5: Boolean,
        h6: Boolean,
    },

    setup ( props ) {
        
        const class_list = computed( () => props.classes ? Object.assign({}, props.classes) : {} )
        const font_size = computed( () => {
            if ( props.h1 ) return '3rem'
            if ( props.h2 ) return '2rem'
            if ( props.h3 ) return '1.5rem'
            if ( props.h4 ) return '1.25rem'
            if ( props.h5 ) return '1.15rem'
            else return '1.1rem'
        })

        return {
            class_list,
            font_size
        }
    }


})
</script>
<style scoped>

.co-title-overline {

    font-size: 0.7em;
    letter-spacing: 1px;
    text-transform: uppercase;
    
}

.co-title-title {

    font-size: 1em;
    font-weight: 600;
    line-height: 1.2;
    letter-spacing: -0.015em;

    padding: 1em 0 0.25em 0;
}

.co-title-subtitle {

    color: var(--co-color-text-tint-2);
    
    font-size: 0.8em;
    line-height: 1.3;

    padding: 0.25em 0 0.5em 0;

}

</style>