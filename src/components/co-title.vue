<template>

<div :class="['co-title', class_list.title_group, inline ? 'co-title-inline' : '']">
    <div :class="['co-title-title', class_list.title]">

        <div :class="['co-title-overline', class_list.overline]">
            {{ overline }}
            <slot name="overline"></slot>
        </div>

        {{ title }}

        <slot></slot>

        <span v-if="side" :class="['co-title-subtitle co-title-subtitle-side', class_list.subtitle]">
            {{ subtitle }}
            <slot name="subtitle-side"></slot>
        </span>
        
    </div>
    <div v-if="!side" :class="['co-title-subtitle', class_list.subtitle]">
        {{ subtitle }}
        <slot name="subtitle"></slot>
    </div>
</div>

</template>
<script>
import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'co-title',

    props: {
        title: String,
        subtitle: String,
        overline: String,

        classes: Object,

        side: Boolean,

        h1: Boolean,
        h2: Boolean,
        h3: Boolean,
        h4: Boolean,
        h5: Boolean,
        h6: Boolean,

        inline: Boolean,
    },

    setup ( props ) {
        
        const class_list = computed( () => props.classes ? Object.assign({}, props.classes) : {} )

        const font_size = computed( () => {
            if ( props.h1 ) return '3rem'
            if ( props.h2 ) return '2rem'
            if ( props.h3 ) return '1.5rem'
            if ( props.h4 ) return '1.25rem'
            if ( props.h5 ) return '1.2rem'
            else return '1.1rem'
        })

        const line_height = computed( () => {
            if ( props.h1 ) return '1'
            if ( props.h2 ) return '1.1'
            if ( props.h3 ) return '1.2'
            if ( props.h4 ) return '1.25'
            if ( props.h5 ) return '1.3'
            else return '1.3'
        })

        const subtitle_font_size = computed( () => {
            if ( props.h1 ) return '0.6em'
            if ( props.h2 ) return '0.7em'
            if ( props.h5 ) return '0.9em'
            if ( props.h6 ) return '1em'
            else return '0.8em'
        })

        const font_weight = computed( () => {
            if ( props.h6 ) return '500'
            else return '600'
        })

        return {
            class_list,
            font_size,
            line_height,
            subtitle_font_size,
            font_weight
        }
    }


})
</script>
<style scoped>

.co-title-inline {
    display: inline-block;
}

.co-title, .co-title-overline, .co-title-subtitle, .co-title-title {
    max-width: 100%;
    box-sizing: border-box;
}

.co-title {
    font-size: v-bind(font_size);
}

.co-title-overline {

    font-size: 0.7em;
    letter-spacing: 1px;
    text-transform: uppercase;
    
}

.co-title-title {

    font-size: 1em;
    font-weight: v-bind(font_weight);
    line-height: v-bind(line_height);
    letter-spacing: -0.015em;

    padding: 1em 0 0.25em 0;
}

.co-title-subtitle {
    
    font-size: v-bind(subtitle_font_size);
    font-weight: 500;
    line-height: v-bind(line_height);

    padding: 0.25em 0;

}

.co-title-subtitle-side {
    margin-left: 0.25em;
}

</style>