<template>

<div :class="['co-card', class_list.card, !no_margin ? 'co-card-margin' : '']">

    <transition-group>
        <div v-show="!hide_before" key="co-card-before">
            <div :class="['co-card-before', class_list.before]">
                <slot name="before"></slot>
            </div>
        </div>
    </transition-group>

    <div v-if="!no_spacer" class="co-card-spacer" />

    <div :class="['co-card-header', class_list.header]">

        <CoTitle :title="title" :subtitle="subtitle" :overline="overline" :classes="class_list" />
    
    </div>


    <div :class="['co-card-content', class_list.content]">

        <slot name="content"></slot>

    </div>

    <div v-if="!no_spacer" class="co-card-spacer" />

    <transition-group>
        <div v-show="!hide_actions" key="co-card-actions">
            <div :class="['actions', class_list.actions]">
                <slot name="actions"></slot>
            </div>
        </div>
    </transition-group>

</div>

</template>
<script>

import { defineComponent, computed } from 'vue'

import CoTitle from './CoTitle'

export default defineComponent({

    name: 'CoCard',

    components: {
        CoTitle,
    },

    props: {

        // Content
        title: String,
        subtitle: String,
        overline: String,

        classes: Object,
        
        dense: Boolean,
        no_margin: Boolean,
        no_spacer: Boolean,

        hide_before: Boolean,
        hide_actions: Boolean,
    },

    setup ( props, { slots } ) {

        const class_list = computed( () => props.classes ? props.classes : {} )

        const has_header = computed( () => slots.header || props.title ? true : false )
        const has_subtitle = computed( () => slots.subtitle || props.subtitle ? true : false )
        const has_overline = computed( () => slots.overline || props.overline ? true : false )
        const has_content = computed( () => slots.contenst ? true : false )
        const has_actions = computed( () => slots.actions ? true : false )

        return {
            class_list,
            has_header,
            has_subtitle,
            has_overline,
            has_content,
            has_actions,
        }

    }

})

</script>

<style scoped>

.co-card-margin {
    margin: 0.5em;
}

.co-card-spacer {
    padding-top: 2.5em;
}

.co-card {

    background: var(--co-color-background);

    flex: 1;

    border-radius: 4em;
    min-height: 8em;
}

.co-card-content {

    color: var(--co-color-text);

    padding: 0.75em;
    line-height: 1.6;
}


</style>