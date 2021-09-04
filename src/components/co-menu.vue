
<template>

<div v-show="show_clickarea" class="co-menu-clickout-area" @click="clicked_out" @keyup.esc="clicked_out" />

<span class="co-menu-group" @mouseenter="mouse_enter" @mouseleave="mouse_leave" @click="clicked">

    <span ref="origin" class="co-menu-origin">

        <!-- Origin/Event Handler -->
        <slot></slot>

        <div v-if="!reduceHoverArea" class="co-menu-hover-area" />

        <div :class="['co-menu-container', right ? 'co-menu-container-right' : center ? 'co-menu-container-center' : 'co-menu-container-left']">
    
            <transition name="co-menu">
                <div v-show="show"  :class="['co-menu', shadow ? 'co-menu-shadow' : shadowDark ? 'co-menu-shadow-dark' : shadowLight ? 'co-menu-shadow-light' : '']">
                    <div :class="['co-menu-triangle', right ? 'co-menu-triangle-right' : center ? 'co-menu-triangle-center' : 'co-menu-triangle-left' ]" />

                    <div class="co-menu-shift" :style="menu_shift">
                        <div class="co-menu-bubble">

                            <!-- Toolbar -->
                            <div v-if="this.$slots.toolbar || this.$slots['toolbar-right']" :class="['co-menu-toolbar', class_list.toolbar]">
                                <div v-if="this.$slots.toolbar" class="co-menu-toolbar-left">
                                    <slot name="toolbar"></slot>
                                </div>
                                <div v-if="this.$slots['toolbar-right']" class="co-menu-toolbar-right">
                                    <slot name="toolbar-right"></slot>
                                </div>
                            </div>

                            <!-- Before Content -->
                            <div :class="['co-menu-before', class_list.before]">
                                <slot name="before"></slot>
                            </div>

                            <!-- Columns -->
                            <div v-if="cols" :class="['co-menu-cols', class_list.cols]">
                                <div v-for="col in cols" :key="`menu-col-${col}`" :class="['co-menu-col', class_list.col]">
                                    <slot :name="`col-${col}`"></slot>                       
                                </div>
                            </div>

                            <!-- Simple Main Content Block -->
                            <div v-if="this.$slots.content" class="co-menu-content">
                                <slot name="content"></slot>
                            </div>

                        </div>
                    </div>
                </div>
            </transition>
        </div>
    </span>

</span>

</template>
<script>

import { defineComponent, watch, computed, ref } from 'vue'

export default defineComponent({

    name: 'co-menu',

    props: {

        width: String,
        height: String,
        viewportWidth: Boolean,
        maxWidth: String,

        left: Boolean,
        right: Boolean,
        center: Boolean,

        cols: Number,

        hover: Boolean,
        reduceHoverArea: Boolean,

        classes: Object,

        bg: String,

        shadowLight: Boolean,
        shadow: Boolean,
        shadowDark: Boolean,

        lessRound: Boolean,

    },

    setup ( props ) {

        const class_list = computed( () => {
            if ( props.classes ) return Object.assign( {}, props.classes )
            else return {}
        })


        const border_radius = computed( () => props.lessRound ? '1.5em' : '3.5em' )

        // Calculates border radius based on the position of the arrow
        const menu_radius = computed( () => {
            let radius = ''
            if ( props.left ) radius += ' 0'
            else radius += ` ${border_radius.value}`
            if ( props.right ) radius += ' 0'
            else radius += ` ${border_radius.value}`
            radius += ` ${border_radius.value} ${border_radius.value}`
            return radius
        })

        const get_width_within_viewport = (origin) => {

            let new_width, viewport_to_element

            const half_element_width = 0.5 * ( origin.getBoundingClientRect().width )
            const viewport_width = document.documentElement.clientWidth
            const padding = 32

            if ( props.left ) {

                viewport_to_element = origin.getBoundingClientRect().left
                new_width = viewport_width - ( viewport_to_element + half_element_width ) - padding

            } else if ( props.right ) {

                viewport_to_element = origin.getBoundingClientRect().right
                const viewport_to_element_left = viewport_width - viewport_to_element

                new_width = viewport_width - viewport_to_element_left - half_element_width - padding
            }

            else if ( props.center ) {

                new_width = viewport_width - ( 2 * padding )

            }

            return new_width

        }

        const menu_width = ref(props.width)

        const menu_shift = ref({})

        const max_width = computed( () => {

            if ( props.maxWidth ) {

                let new_max_width = parseInt(props.maxWidth)
                const viewport = document.documentElement.clientWidth

                if ( props.maxWidth.includes('vw') ) {
                    new_max_width = new_max_width * (viewport/100)
                }

                return new_max_width
                
            } else return 0
        })

        // When using a centered menu, the contents will occasionally go off-screen. This function
        // shifts the menu to fit on screen.
        const get_menu_shift = (origin) => {

            const element_width = parseInt(menu_width.value)
            const element_max_width = max_width.value

            const width = element_max_width === 0 ? element_width : element_width < element_max_width ? element_width : element_max_width

            const viewport_to_element_left = origin.getBoundingClientRect().left
            const viewport_to_element_right = origin.getBoundingClientRect().right
            const viewport_to_element_center = ( ( viewport_to_element_right - viewport_to_element_left ) * 0.5 ) + viewport_to_element_left

            console.log(viewport_to_element_center, width, ( viewport_to_element_center - (width * 0.5) ))

            // No need to shift the menu if it already fully fits in the viewport
            if ( ( ( viewport_to_element_center + (width * 0.5) ) > document.documentElement.clientWidth ) || ( viewport_to_element_center - (width * 0.5) < 0 ) ) {
                
                const viewport_shift_value = ( 32 - ( viewport_to_element_center - ( width * 0.5 ) ) )
                const max_shift_value = ( width * 0.5 ) - 64 

                let shift_value = Math.abs(viewport_shift_value) <= Math.abs(max_shift_value) ? viewport_shift_value : ( Math.sign(viewport_shift_value) * max_shift_value )
                if ( Math.sign(shift_value) === 1 ) shift_value += 96

                shift_value = ` ${shift_value}px`

                console.log(width, shift_value)

                return {
                    position: 'absolute',
                    left: shift_value
                }
            } else {
                console.log('...')
                return {}
            }
        }

        const to_show = ref(false)
        const show = ref(false)
        const show_clickarea = ref(false)

        // `to_show` is used to debounce the menu's opening and closing
        // This is to avoid stuttering
        const show_menu = () => {
            return setTimeout( () => {
                show.value = to_show.value
            }, 100)
        }

        // Controls hover-to-open menus
        const mouse_enter = () => {
            if ( props.hover ) to_show.value = true
        }
        const mouse_leave = () => {
            if ( props.hover ) to_show.value = false
        }

        // Controls all menus: they are all click-to-open on touchscreen
        const clicked = (event) => {
            if ( show.value ) {
                
                // If the click event was somewhere on the dropdown, we don't want to close it.
                const path = event.path.findIndex( target => target.className && target.className.includes('co-menu-container') )
                if ( path === -1 ) {
                    to_show.value = false
                    show_clickarea.value = false
                }

            } else {
                to_show.value = true
                show_clickarea.value = true
            }
        }

        const clicked_out = () => {
            to_show.value = false
            show.value = false
            show_clickarea.value = false
        }

        watch(to_show, show_menu)

        return {
            class_list,
            border_radius,
            menu_radius,

            get_width_within_viewport,
            menu_width,
            menu_shift,
            get_menu_shift,

            show,
            to_show,
            show_clickarea,

            mouse_enter,
            mouse_leave,
            clicked,
            clicked_out,
        }
    },

    mounted () {

        if ( this.viewportWidth ) {
            this.menu_width = this.get_width_within_viewport(this.$refs.origin).toString()+'px'

            if ( this.center ) {
                this.menu_shift = this.get_menu_shift(this.$refs.origin)
            }
        }
    },

    watch: {

        to_show () {
            // Reset menu width and shift values every show/hide, in case of viewport changes
            if ( this.viewPortWidth ) {
                this.menu_width = this.get_width_within_viewport(this.$refs.origin).toString()+'px'

                if ( this.center ) {
                    this.menu_shift = this.get_menu_shift(this.$refs.origin)
                }
            }

        }
    }
})

</script>

<style lang="scss" scoped>

.co-menu-container,
.co-menu,
.co-menu-content,
.co-menu-group {
    box-sizing: border-box;
}

.co-menu-group, .co-menu-origin {
    position: relative;
    width: inherit;
}

.co-menu-container {

    width: v-bind(menu_width);
    max-width: v-bind(maxWidth);
    padding: 8px 0 0 0;

    position: absolute;
    z-index: 1000;
}

.co-menu-container-left {
    left: 50%;
}

.co-menu-container-right {
    right: 50%;
}

.co-menu-container-center {
    left: 50%;
    transform: translate(-50%, 0);
}

.co-menu-hover-area {

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

.co-menu-clickout-area {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}


.co-menu {

    display: block;

    width: v-bind(menu_width);
    max-width: v-bind(maxWidth);
    height: v-bind(height);

    position: relative;
    
}

.co-menu-shift {

    min-height: 8em;
    width: v-bind(menu_width);
    max-width: v-bind(maxWidth);
}

.co-menu-bubble {

    background: v-bind(bg);
    border-radius: v-bind(menu_radius);

    display: block;

    position: relative;

    min-height: 8em;
    width: v-bind(menu_width);
    max-width: v-bind(maxWidth);
    height: v-bind(height);
    margin-bottom: 2em;
    margin-right: 2em;
}

.co-menu-toolbar {
    display: flex;
    align-items: center;
    padding: 1.75em 1.5em 0.25em 1.5em;
    box-sizing: border-box;
}

.co-menu-toolbar-left {
    flex: 1 auto;
    align-self: center;
    display: flex;
    align-items: center;
}

.co-menu-toolbar-right {
    flex: 1 auto;
    align-self: center;
    text-align: right;
    margin-left: 1.5em;
}

.co-menu-cols {
    position: relative;
    display: flex;
    box-sizing: border-box;
    height: 100%;
    min-height: 8em;
}

.co-menu-col {
    flex: 1 auto;
    box-sizing: border-box;
}


.co-menu-shadow-light {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.15);
}

.co-menu-shadow {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.3);
}

.co-menu-shadow-dark {
    box-shadow: 0px 10px 30px -20px rgba(0, 0, 0, 0.7);
}

.co-menu-content {

    padding: 2em 1.5em;

}

.co-menu-triangle {
    width: 0;
    height: 0;
    border-style: solid;
    border-color: transparent transparent v-bind(bg) transparent;

    position: absolute;
    top: -16px;
    z-index: 100;
}

.co-menu-triangle-left {
    border-width: 0 32px 16px 0px;
}

.co-menu-triangle-right {
    right: 0;
    border-width: 0 0 16px 32px;
}

.co-menu-triangle-center {
    left: 50%;
    transform: translate(-50%, 0);
    border-width: 0 32px 32px 32px;
}

.co-menu-enter-active,
.co-menu-leave-active {
    transition: 250ms ease;

    .co-menu {
        transition: 150ms ease;
        transform: scaleY(100%);
        transform-origin: top;
    }
}

.co-menu-enter-from,
.co-menu-leave-to {
    transform: translateY(-0.75em);
    opacity: 0;

    .co-menu {
        transform: scaleY(75%);
        transform-origin: top;
    }
}

</style>