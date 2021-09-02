<template>

<div :class="['co-card-container', !noMargin ? 'co-card-margin' : '']">
<div :class="['co-card', class_list.card, shadow ? 'co-card-shadow' : '']">

    <!-- `co-card-top` container -->
    <div v-if="has_header" :class="['co-card-top', class_list.top]">

        <div v-if="!has_toolbar && !noSpacer" class="co-card-spacer" />

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
            <div class="co-card-toolbar-dense">
                <div class="co-card-toolbar-left">
                    <slot name="header"></slot>
                </div>
                <div class="co-card-toolbar-right">
                    <slot name="header-right"></slot>
                </div>
            </div>
        </div>

    </div>

    <div v-if="has_before_content" :class="['co-card-before-content', class_list.before, only_before_content ? 'co-card-border-radius' : '']">
        <!-- #before slot -->
        <slot name="before"></slot>
    </div>

    <!-- `co-card-content` container -->
    <div v-if="has_content" :class="['co-card-content', class_list.content]">

        <!-- #content slot -->
        <slot name="content"></slot>

    </div>

    <div v-if="!has_actions && !noSpacer" class="co-card-spacer" />

    <!-- `co-card-actions` container -->
    <div v-if="has_actions" :class="['co-card-actions', class_list.actions]">

        <!-- #actions slot -->
        <div class="co-card-toolbar-left">
            <slot name="actions"></slot>
        </div>
        <div class="co-card-toolbar-right">
            <slot name="actions-right"></slot>
        </div>

    </div>
</div>
</div>

</template>
<script>

import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'CoCard',

    props: {

        // Style
        classes: Object,

        dense: Boolean,
        noMargin: Boolean,
        noSpacer: Boolean,
        shadow: Boolean,

    },

    setup ( props, { slots } ) {

        const class_list = computed( () => props.classes ? props.classes : {} )

        const has_toolbar = computed( () => slots.toolbar || slots.toolbarRight )
        const has_header = computed( () => slots.header || slots.headerRight )
        const has_before_content = computed( () => slots.before )
        const has_content = computed( () => slots.content )
        const has_actions = computed( () => slots.actions || slots.actionsRight )

        const only_before_content = computed( () => has_before_content.value && !has_toolbar.value && !has_header.value && !has_content.value && !has_actions.value )

        return {
            class_list,
            has_toolbar,
            has_header,
            has_before_content,
            only_before_content,
            has_content,
            has_actions,
        }

    }

})

</script>

<style scoped>

.co-card-container, 
.co-card-margin, 
.co-card, 
.co-card-top, 
.co-card-toolbar,
.co-card-header, 
.co-card-before-content, 
.co-card-content, 
.co-card-actions {
    box-sizing: border-box;
    max-width: 100%;
    width: 100%;
}

.co-card-margin {
    margin: 0.5em;
}

.co-card-spacer {
    padding-top: 1.5em;
}

.co-card-border-radius {
    border-radius: 3.5em;
}

.co-card-container {
    flex: 1;
    position: relative;
}

.co-card {

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

}

.co-card-toolbar {
    display: flex;
    padding: 1.75em 2.5em 0.25em 2.5em;
}

.co-card-toolbar-dense {
    display: flex;
}

.co-card-toolbar-left {
    flex: 1 auto;
}

.co-card-toolbar-right {
    flex: 1 auto;
    align-self: center;
    text-align: right;
    margin-left: 1.5em;
}

.co-card-header {
    padding: 0.25em 0.75em 0.25em 0.75em;
}

.co-card-before-content {
    flex: 1;
}

.co-card-content {

    /* Text */
    line-height: 1.6;

    /* Box Style */
    padding: 0.75em 0.75em 1.5em 0.75em;

    /* Positioning */
    flex: 1;
}

.co-card-actions {

    /* Box Style */
    border-radius: 0 0 3.5em 3.5em;
    padding: 0.75em 2em 1.25em 2em;

    /* Positioning */
    flex: 1;
    align-self: flex-end;
    display: flex;

    /* Sizing */
    min-height: 3.5em;
    

}


</style>