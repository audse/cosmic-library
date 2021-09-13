<template>

<article :class="['container', classList.container]">
<section :class="['co-card', classList.card, shadowLight ? 'shadow-light' : shadowDark ? 'shadow-dark' : shadow ? 'shadow' : '']">


    <!-- Adds padding (because of the large border-radius) before the content, if not toolbar exists -->
    <div v-if="!has.header && !has.toolbar && !noSpacer" class="spacer" />
    <!-- `top` container -->
    <header v-if="has.header" :class="[classList.top]">

        <!-- Adds padding (because of the large border-radius) before the header content/toolbar -->
        <div v-if="!has.toolbar && !noSpacer" class="spacer" />

        <nav v-if="has.toolbar" class="toolbar">
            <section class="toolbar-left">
                <slot name="toolbar"></slot>
            </section>
            <section v-if="has.toolbarRight" class="toolbar-right">
                <slot name="toolbar-right"></slot>
            </section>
        </nav>

        <!-- `header` container -->
        <section :class="['header', classList.header]">
            <section class="toolbar-left">
                <slot name="header"></slot>
            </section>
            <section  v-if="has.headerRight" class="toolbar-right">
                <slot name="header-right"></slot>
            </section>
        </section>

    </header>

    <!-- Adds padding (because of the large border-radius) before the content, if not toolbar exists -->
    <div v-if="!has.header && !has.toolbar && !noSpacer" class="spacer" />

    <section v-if="has.before" :class="['before-content', classList.before, hasOnlyBefore ? 'border-radius' : '']">
        <!-- #before slot -->
        <slot name="before"></slot>
    </section>

    <!-- `content` container -->
    <section v-if="has.content" :class="['content', classList.content]">

        <!-- #content slot -->
        <slot></slot>

    </section>

    <!-- Adds padding (because of the large border-radius) before the actions -->
    <div v-if="!has.actions && !noSpacer" class="spacer" />

    <!-- `actions` container -->
    <footer v-if="has.actions" :class="['actions', classList.actions]">

        <!-- #actions slot -->
        <nav class="toolbar-left">
            <slot name="actions"></slot>
        </nav>
        <nav  v-if="has.actionsRight" class="toolbar-right">
            <slot name="actions-right"></slot>
        </nav>

    </footer>

</section>
</article>

</template>
<script>

import { defineComponent, computed, reactive } from 'vue'

export default defineComponent({

    name: 'co-card',

    props: {

        // Style
        classes: Object,
        bg: String,

        dense: Boolean,

        lessRound: Boolean,
        noSpacer: Boolean,
        shadow: Boolean,
        shadowLight: Boolean,
        shadowDark: Boolean,

    },

    setup ( props, { slots } ) {

        const classList = computed( () => props.classes ? props.classes : {} )

        const has = reactive({
            toolbar: slots.toolbar || slots['toolbar-right'] ? true : false,
            toolbarRight: slots['toolbar-right'] ? true : false,
            header: slots.header || slots['header-right'] ? true : false,
            headerRight: slots['header-right'] ? true : false,
            before: slots.before ? true : false,
            content: slots.default ? true : false,
            actions: slots.actions || slots['actions-right'] ? true : false,
            actionsRight: slots['actions-right'] ? true : false,
        })

        const hasOnlyBefore = computed( () => {
            return ( 
                !has.toolbar && 
                !has.header && 
                !has.content && 
                !has.actions && 
                has.before
            )
        })

        const borderRadius = computed( () => props.lessRound ? '1.5em' : '3.5em' )

        const background = computed( () => props.bg ? props.bg : 'initial')

        return {
            classList,

            has,
            hasOnlyBefore,
            
            borderRadius,
            background
        }

    }

})

</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
    display: block;
    width: 100%;
    height: fit-content;
}

.spacer {
    padding-top: v-bind(borderRadius);
}

.border-radius {
    border-radius: v-bind(borderRadius);
}

.container {
    flex: 1 auto;
    position: relative;
}

.co-card {

    background: v-bind(background);

    display: flex;
    flex-direction: column;

    border-radius: v-bind(borderRadius);
    min-height: 8em;
    height: auto;
}

.shadow-light {
    box-shadow: 0px 5px 15px -10px rgba(0, 0, 0, 0.15);
}

.shadow {
    box-shadow: 0px 5px 15px -10px rgba(0, 0, 0, 0.3);
}

.shadow-dark {
    box-shadow: 0px 5px 20px -15px rgba(0, 0, 0, 0.7);
}

header {
    
    /* Box Style */
    border-radius: v-bind(borderRadius) v-bind(borderRadius) 0 0;
    display: block;

    /* Positioning */
    flex: 1 auto;
    
    /* Sizing */
    min-height:  v-bind(borderRadius);

}

.toolbar {
    display: flex;
    align-items: center;
    padding: 1.75em 2.5em 0.25em 2.5em;
}

.toolbar-left, .toolbar-right {
    flex: 1 auto;
    align-self: center;
}

.toolbar-right {

    width: fit-content;

    /* Right Align */
    text-align: right;
    justify-content: right;
    justify-self: right;

    /* Left Spacing */
    padding-left: 1.5em;
}

.header {
    padding: 0.25em 0.75em 0.25em 0.75em;
    display: flex;
}

.before-content {
    flex: 1 auto;
}

.content {

    /* Text */
    line-height: 1.6;

    /* Box Style */
    padding: 0.75em 0.75em 1.5em 0.75em;

    /* Positioning */
    flex: 1 auto;
}

.actions {

    /* Box Style */
    border-radius: 0 0  v-bind(borderRadius)  v-bind(borderRadius);
    padding: 0.75em 2em 1.25em 2em;

    /* Positioning */
    flex: 1 auto;
    align-self: flex-end;
    display: flex;

    /* Sizing */
    min-height: v-bind(borderRadius);
    width: 100%;
    

}


</style>