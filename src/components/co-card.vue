<template>

<div :class="['co-card-container', !no_margin ? 'co-card-margin' : '']">
<div :class="['co-card', class_list.card, shadow ? 'co-card-shadow' : '']">

    <!-- `co-card-top` container -->
    <div v-if="has_header" :class="['co-card-top', class_list.top]">

        <div v-if="!has_toolbar" class="co-card-spacer" />

        <div v-if="has_toolbar" class="co-card-toolbar">
            <div class="co-card-toolbar-left">
                <slot name="toolbar"></slot>
            </div>
            <div class="co-card-toolbar-right">
                <slot name="toolbar-right"></slot>
            </div>
        </div>

        <!-- `co-card-header` container -->
        <div :class="['co-card-header', class_list.header]">
            <slot name="header"></slot>
        </div>

    </div>

    <!-- #before-content slot -->
    <slot name="before-content"></slot>

    <!-- `co-card-content` container -->
    <div v-if="has_content" :class="['co-card-content', class_list.content]">

        <!-- #content slot -->
        <slot name="content"></slot>

    </div>

    <div v-if="!has_actions" class="co-card-spacer" />

    <!-- `co-card-actions` container -->
    <div v-if="has_actions" :class="['co-card-actions', class_list.actions]">

        <!-- #actions slot -->
        <slot name="actions"></slot>

    </div>
</div>
</div>

</template>
<script>

import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'CoCard',

    props: {

        // Content
        title: String,
        subtitle: String,
        overline: String,

        // Style
        classes: Object,
        dense: Boolean,
        no_margin: Boolean,
        no_spacer: Boolean,
        shadow: Boolean,

    },

    setup ( props, { slots } ) {

        const class_list = computed( () => props.classes ? props.classes : {} )

        const has_toolbar = computed( () => slots.toolbar || slots['toolbar-right'] ? true : false )
        const has_header = computed( () => slots.header || props.title || props.subtitle || props.overline ? true : false )
        const has_subtitle = computed( () => slots.subtitle || props.subtitle ? true : false )
        const has_overline = computed( () => slots.overline || props.overline ? true : false )
        const has_content = computed( () => slots.content ? true : false )
        const has_actions = computed( () => slots.actions ? true : false )

        return {
            class_list,
            has_toolbar,
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

* {
    box-sizing: border-box;
}

.co-card-margin {
    margin: 0.5em;
}

.co-card-spacer {
    padding-top: 1.5em;
}

.co-card-container {
    flex: 1;
    position: relative;
    width: 100%;
}

.co-card {

    background: rgb(var(--co-color-background));

    display: flex;
    flex-direction: column;

    border-radius: 3.5em;
    min-height: 8em;
    height: auto;
}

.co-card-shadow {
    box-shadow: 0px 5px 15px -10px rgba(0, 0, 0, 0.1);
}

.co-card-top {
    
    /* Box Style */
    border-radius: 3.5em 3.5em 0 0;

    /* Positioning */
    flex: 1;
    
    /* Sizing */
    min-height: 3.5em;
    width: 100%;

}

.co-card-toolbar {
    display: flex;
    padding: 1.75em 2em 0.25em 2em;
    width: 100%;
}

.co-card-toolbar-left {
    flex: 1 auto;
}

.co-card-toolbar-right {
    flex: 1 auto;
    align-self: flex-end;
    text-align: right;
}

.co-card-header {
    padding: 0.25em 0.75em 0.25em 0.75em;
}

.co-card-content {

    /* Text */
    color: var(--co-color-text-tint-1);
    line-height: 1.6;

    /* Box Style */
    padding: 0.75em 0.75em 1.5em 0.75em;

    /* Positioning */
    flex: 1;

    /* Sizing */
    width: 100%;
}

.co-card-actions {

    /* Content */
    text-align: center;

    /* Box Style */
    border-radius: 0 0 3.5em 3.5em;
    padding: 0.8em 2em;

    /* Positioning */
    flex: 1;
    align-self: flex-end;

    /* Sizing */
    width: 100%;
    min-height: 3.5em;
    

}


</style>