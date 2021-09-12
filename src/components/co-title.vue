<template>

<header :class="[classList.titleGroup, inline ? 'inline' : '']">
    <main :class="[classList.title]">

        <strong :class="[classList.overline]">
            {{ overline }}
            <slot name="overline"></slot>
        </strong>

        {{ title }}

        <slot></slot>

        <aside v-if="side" :class="[classList.subtitle]">
            {{ subtitle }}
            <slot name="subtitle-side"></slot>
        </aside>
        
    </main>
    <p v-if="!side" :class="[classList.subtitle]">
        {{ subtitle }}
        <slot name="subtitle"></slot>
    </p>
</header>

</template>
<script>
import { defineComponent, computed, reactive } from 'vue'

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
        
        const classList = reactive( props.classes ? props.classes : {} )

        const titleFontSize = computed( () => {
            if ( props.h1 ) return '3rem'
            else if ( props.h2 ) return '2rem'
            else if ( props.h3 ) return '1.5rem'
            else if ( props.h4 ) return '1.25rem'
            else if ( props.h5 ) return '1.2rem'
            else if ( props.h6 ) return '1.1rem'
            else return '1rem'
        })

        const lineHeight = computed( () => {
            if ( props.h1 ) return '1'
            if ( props.h2 ) return '1.1'
            if ( props.h3 ) return '1.2'
            if ( props.h4 ) return '1.25'
            if ( props.h5 ) return '1.3'
            else return '1.3'
        })

        const subtitleFontSize = computed( () => {
            if ( props.h1 ) return '0.6em'
            if ( props.h2 ) return '0.7em'
            if ( props.h5 ) return '0.9em'
            if ( props.h6 ) return '0.95em'
            else return '0.8em'
        })

        const fontWeight = computed( () => {
            if ( props.h6 ) return '500'
            else return '600'
        })

        return {
            classList,
            titleFontSize,
            lineHeight,
            subtitleFontSize,
            fontWeight
        }
    }


})
</script>
<style scoped>

* {
    box-sizing: border-box;
    max-width: 100%;
    display: block;
    height: fit-content;
    margin: 0;
    padding: 0;
}

header {
    font-size: v-bind(titleFontSize);
}

header.inline {
    display: inline-block;
    width: fit-content;
}

/* Title */
main {
    font-size: 1em;
    font-weight: v-bind(fontWeight);
    line-height: v-bind(lineHeight);
    letter-spacing: -0.015em;

    padding: 1em 0 0.25em 0;
}

/* Subtitle */
p, aside {
    font-size: v-bind(subtitleFontSize);
    font-weight: 500;
    line-height: v-bind(lineHeight);

    padding: 0.25em 0;
}

/* Subtitle (side) */
aside {
    margin-left: 0.25em;
}

/* Overline */
strong {
    font-size: 0.7em;
    letter-spacing: 1px;
    text-transform: uppercase;
    font-weight: v-bind(fontWeight);
}

</style>