
<template>

<nav v-show="showClickArea" class="clickout-area" @click="clickedOut" @keyup.esc="clickedOut" @keyup.enter="clickedOut" tabindex="0" />

<span :class="['group', classList.group]" @mouseenter="mouseEnter" @mouseleave="mouseLeave">

    <span ref="origin" class="origin">

        <!-- Origin/Event Handler -->
        <button @click="clicked" tabindex="0" @keyup.enter="clicked">
            <slot></slot>
        </button>

        <nav v-if="!reduceHoverArea && hover" class="hover-area" tabindex="0" @keyup.enter="mouseLeave" />

        <section :class="['container', right ? 'container-right' : center ? 'container-center' : 'container-left']">
    
            <transition name="menu">
                <section v-show="show" class="menu">
                    <figure v-if="!noArrow" :class="['triangle', right ? 'triangle-right' : center ? 'triangle-center' : 'triangle-left', classList.arrow  ]" />

                    <section class="shift" :style="menuShift">
                        <article :class="['bubble', shadow ? 'shadow' : shadowDark ? 'shadow-dark' : shadowLight ? 'shadow-light' : '', classList.menu]">

                            <!-- Toolbar -->
                            <nav v-if="this.$slots.toolbar || this.$slots['toolbar-right']" :class="['toolbar', classList.toolbar]">
                                <section v-if="this.$slots.toolbar" :class="['toolbar-left', classList.toolbar]">
                                    <slot name="toolbar" :coMenu="coMenu"></slot>
                                </section>
                                <section v-if="this.$slots['toolbar-right']" class="toolbar-right">
                                    <slot name="toolbar-right" :coMenu="coMenu"></slot>
                                </section>
                            </nav>

                            <!-- Spacer -->
                            <div v-if="!this.$slots.toolbar && !this.$slots['toolbar-right'] && this.$slots.header" class="spacer" />

                            <!-- Header -->
                            <header v-if="this.$slots.header" :class="[classList.header]">
                                <slot name="header" :coMenu="coMenu"></slot>
                            </header>

                            <!-- Before Content -->
                            <section :class="['before', classList.before, onlyBefore ? 'before-only' : '']">
                                <slot name="before" :coMenu="coMenu"></slot>
                            </section>

                            <!-- Columns -->
                            <section v-if="cols" :class="['cols', classList.cols]">
                                <aside v-for="col in cols" :key="`menu-col-${col}`" :class="['col', classList.col, classList[`col-${col}`], !noColPadding ? 'col-padding' : '']">
                                    <slot :name="`col-${col}`" :coMenu="coMenu"></slot>                       
                                </aside>
                            </section>

                            <!-- Simple Main Content Block -->
                            <main v-if="this.$slots.main" :class="[classList.main]">
                                <slot name="content" :coMenu="coMenu"></slot>
                            </main>

                        </article>
                    </section>
                </section>
            </transition>
        </section>
    </span>

</span>

</template>
<script>

import { defineComponent, watch, computed, ref, reactive } from 'vue'

export default defineComponent({

    name: 'co-menu',

    props: {

        width: String,
        height: String,

        zIndex: Number,

        viewportWidth: Boolean,
        maxWidth: String,

        left: Boolean,
        right: Boolean,
        center: Boolean,

        arrowOverlap: String,

        startOpen: Boolean,

        hover: Boolean,
        reduceHoverArea: Boolean,

        cols: Number,

        classes: Object,

        bg: String,

        shadowLight: Boolean,
        shadow: Boolean,
        shadowDark: Boolean,

        lessRound: Boolean,
        noColPadding: Boolean,
        noSpacer: Boolean,
        noArrow: Boolean,

    },

    emits: ['coMenuOpened', 'coMenuClosed'],

    setup ( props, { slots, emit } ) {

        const classList = reactive(  props.classes ? props.classes : {} )

        const groupZIndex = computed( () => props.zIndex ? props.zIndex : 1000 )
        const arrowOverlapValue = computed( () => props.arrowOverlap ? props.arrowOverlap : '0px')
        const borderRadius = computed( () => props.lessRound ? '1.5em' : '3.5em' )

        // Calculates border radius based on the position of the arrow
        const menuRadius = computed( () => {
            let radius = ''
            if ( props.left ) radius += ' 0'
            else radius += ` ${borderRadius.value}`
            if ( props.right ) radius += ' 0'
            else radius += ` ${borderRadius.value}`
            radius += ` ${borderRadius.value} ${borderRadius.value}`
            return radius
        })

        const getWidthWithinViewport = (origin) => {

            let newWidth, viewportToElement

            const halfElementWidth = 0.5 * ( origin.getBoundingClientRect().width )
            const viewportWidth = document.documentElement.clientWidth
            const padding = 32

            if ( props.left ) {

                viewportToElement = origin.getBoundingClientRect().left
                newWidth = viewportWidth - ( viewportToElement + halfElementWidth ) - padding

            } else if ( props.right ) {

                viewportToElement = origin.getBoundingClientRect().right
                const viewportToElementLeft = viewportWidth - viewportToElement

                newWidth = viewportWidth - viewportToElementLeft - halfElementWidth - padding
            }

            else if ( props.center ) {

                newWidth = viewportWidth - ( 2 * padding )

            }

            return newWidth

        }

        const menuWidth = ref(props.width)

        const menuShift = ref({})

        const maxWidth = computed( () => {

            if ( props.maxWidth ) {

                let newMaxWidth = parseInt(props.maxWidth)
                const viewport = document.documentElement.clientWidth

                if ( props.maxWidth.includes('vw') ) {
                    newMaxWidth = newMaxWidth * (viewport/100)
                }

                return newMaxWidth
                
            } else return 0
        })

        // When using a centered menu, the contents will occasionally go off-screen. This function
        // shifts the menu to fit on screen.
        const getMenuShift = (origin) => {

            const elementWidth = parseInt(menuWidth.value)
            const elementMaxWidth = maxWidth.value

            const width = elementMaxWidth === 0 ? elementWidth : elementWidth < elementMaxWidth ? elementWidth : elementMaxWidth

            const viewportToElementLeft = origin.getBoundingClientRect().left
            const viewportToElementRight = origin.getBoundingClientRect().right
            const viewportToElementCenter = ( ( viewportToElementRight - viewportToElementLeft ) * 0.5 ) + viewportToElementLeft

            // No need to shift the menu if it already fully fits in the viewport
            if ( ( ( viewportToElementCenter + (width * 0.5) ) > document.documentElement.clientWidth ) || ( viewportToElementCenter - (width * 0.5) < 0 ) ) {
                
                const viewportShiftValue = ( 32 - ( viewportToElementCenter - ( width * 0.5 ) ) )
                const maxShiftValue = ( width * 0.5 ) - 64 

                let shiftValue = Math.abs(viewportShiftValue) <= Math.abs(maxShiftValue) ? viewportShiftValue : ( Math.sign(viewportShiftValue) * maxShiftValue )
                if ( Math.sign(shiftValue) === 1 ) shiftValue += 96

                shiftValue = ` ${shiftValue}px`

                return {
                    position: 'absolute',
                    left: shiftValue
                }
            } else {
                return {}
            }
        }

        const toShow = ref(props.startOpen ? true : false)
        const show = ref(props.startOpen ? true : false)
        const showClickArea = ref(props.startOpen ? true : false)

        // `toShow` is used to debounce the menu's opening and closing
        // This is to avoid stuttering
        const showMenu = () => {
            return setTimeout( () => {
                show.value = toShow.value
                if ( show.value ) {
                    emit ('coMenuOpened')
                } else {
                    emit ('coMenuClosed')
                }
            }, 100)
        }

        // Controls hover-to-open menus
        const mouseEnter = () => {
            if ( props.hover ) toShow.value = true
        }
        const mouseLeave = () => {
            if ( props.hover ) toShow.value = false
        }

        // Controls all menus: they are all click-to-open on touchscreen
        const clicked = (event) => {
            if ( show.value ) {
                
                // If the click event was somewhere on the dropdown, we don't want to close it.
                const path = event.path.findIndex( target => target.className && target.className.includes('menu') )
                if ( path === -1 ) {
                    toShow.value = false
                    showClickArea.value = false
                }

            } else {
                toShow.value = true
                showClickArea.value = true
            }
        }

        const clickedOut = () => {
            toShow.value = false
            showClickArea.value = false
        }

        const coMenu = {
            showMenu,
            mouseEnter,
            mouseLeave,
            clicked,
            clickedOut,
        }

        watch(toShow, showMenu)

        const onlyBefore = computed( () => {
            if ( slots.before && slots.default && Object.keys(slots).length === 2 ) return true
            else return false
        })

        return {
            classList,
            groupZIndex,
            arrowOverlapValue,
            borderRadius,
            menuRadius,

            getWidthWithinViewport,
            menuWidth,
            menuShift,
            getMenuShift,

            show,
            toShow,
            showClickArea,

            mouseEnter,
            mouseLeave,
            clicked,
            clickedOut,
            coMenu,

            onlyBefore
        }
    },

    mounted () {

        if ( this.viewportWidth ) {
            this.menuWidth = this.getWidthWithinViewport(this.$refs.origin).toString()+'px'

            if ( this.center ) {
                this.menuShift = this.getMenuShift(this.$refs.origin)
            }
        }
    },

    watch: {

        toShow () {
            // Reset menu width and shift values every show/hide, in case of viewport changes
            if ( this.viewPortWidth ) {
                this.menuWidth = this.getWidthWithinViewport(this.$refs.origin).toString()+'px'

                if ( this.center ) {
                    this.menuShift = this.getMenuShift(this.$refs.origin)
                }
            }

        }
    }
})

</script>

<style lang="scss" scoped>

* {

    /* Box Model */
    box-sizing: border-box;
    display: block;
    margin: 0;
    padding: 0;

    /* Sizing */
    position: relative;
    width: 100%;
    height: auto;
}

/* Button Reset */
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
    display: inline;

    &:focus-visible {
        outline: auto;
    }
}

.group {
    /* Stacking */
    isolation: isolate;
    z-index: v-bind(groupZIndex);
}

.group, .origin {
    position: relative;
    width: inherit;
}

.container {

    /* Box Model */
    padding: 16px 0 0 0;

    /* Positioning */
    position: absolute;

    /* Sizing */
    width: v-bind(menuWidth);
    max-width: v-bind(maxWidth);
    
    /* Stacking */
    z-index: 10;
}

.container-left {
    left: 50%;
}

.container-right {
    right: 50%;
}

.container-center {
    left: 50%;
    transform: translate(-50%, 0);
}

.hover-area {

    /* Positioning */
    position: absolute;
    top: -2em;
    left: -2em;
    z-index: 0;

    /* Size */
    padding: 2em;
    width: 100%;
    height: 150%;
}

/* When focusing (accessibility), increase the hover area so that the menu won't stutter */
button:focus-visible {
    .hover-area {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }
}

.clickout-area {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}


.menu {

    display: block;

    width: v-bind(menuWidth);
    max-width: v-bind(maxWidth);
    height: v-bind(height);

    position: relative;
    
}

.shift {

    min-height: 8em;
    width: v-bind(menuWidth);
    max-width: v-bind(maxWidth);
}

.bubble {

    background-color: v-bind(bg);
    border-radius: v-bind(menuRadius);

    display: block;
    box-sizing: border-box;

    position: relative;

    min-height: 8em;
    width: v-bind(menuWidth);
    max-width: v-bind(maxWidth);
    height: v-bind(height);
    margin-bottom: 2em;
    margin-right: 2em;
    z-index: 1;
}

/*
*
* TRIANGLE/ARROW
*
*/

/* Figure Reset */
figure {
    margin-block-start: 0;
    margin-block-end: 0;
    margin-inline-start: 0;
    margin-inline-end: 0;
}

.triangle {

    /* Box Model */
    display: inline-block;
    border-style: solid;

    /* Styling */
    color: transparent !important;
    background: transparent !important;
    background-color: transparent !important;

    /* Positioning */
    position: absolute;
    top: calc( -32px + v-bind(arrowOverlapValue) );
    z-index: 2;

    /* Sizing */
    width: 0;
    height: 0;

}

.triangle-left {
    left: 0;
    border-width: 0 32px 32px 0px;
    border-color: transparent transparent v-bind(bg) transparent;
}

.triangle-right {
    right: 0;
    border-width: 0 0 32px 32px;
    border-color: transparent transparent v-bind(bg) transparent;
}

.triangle-center {
    left: 50%;
    transform: translate(-50%, 0);
    border-width: 0 32px 32px 32px;
    border-color: transparent transparent v-bind(bg) transparent;
}

.shadow-light {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.15);
}

.shadow {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.3);
}

.shadow-dark {
    box-shadow: 0px 10px 30px -20px rgba(0, 0, 0, 0.7);
}

/*
*
* SLOTS
*
*/

.spacer {
    padding: 2em;
}

// Before
.before-only {
    width: v-bind(menuWidth);
    max-width: v-bind(maxWidth);
    border-radius: v-bind(menuRadius);
    height: v-bind(height);
    min-height: 8em;
    box-sizing: border-box;
}

// Top Toolbar
.toolbar {
    display: flex;
    align-items: center;
    padding: 1.75em 1.5em 0.25em 1.5em;
    box-sizing: border-box;
}
.toolbar-left {
    flex: 1 auto;
    align-self: center;
    text-align: left;
}
.toolbar-right {
    flex: 1 auto;
    align-self: center;
    text-align: right;
    margin-left: 1.5em;
}

// Columns Layout
.cols {
    position: relative;
    display: flex;
    box-sizing: border-box;
    height: 100%;
    min-height: 8em;
}
.col {
    flex: 1 auto;
    box-sizing: border-box;
}
.col-padding {
    padding: 0.25em 0.25em 2em 0.25em;

    &:first-of-type {
        padding-left: 2em;
    }
    &:last-of-type {
        padding-right: 1em;
    }
}

// Header Slot
header {
    padding: 0 2.5em 2em 1.5em;
    text-align: left;
}

// Main Simple Content Slot
main {
    padding: 0 2.5em 2em 1.5em;
    text-align: left;
}


.menu-enter-active,
.menu-leave-active {
    transition: 250ms ease;

    section.menu {
        transition: 150ms esase;
        transform: scaleY(100%);
        transform-origin: top;

        figure {
            transform: scale(100%);
        }
    }
}

.menu-enter-from,
.menu-leave-to {
    transform: translateY(-0.75em);
    opacity: 0;

    section.menu {
        transform: scaleY(75%);
        transform-origin: top;

        figure {
            transform: scale(100%);
        }
    }
}

</style>