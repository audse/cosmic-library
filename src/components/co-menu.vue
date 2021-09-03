
<template>

<div v-show="show_clickarea" class="co-menu-clickout-area" @click="clicked_out" />

<span class="co-menu-group" @mouseenter="mouse_enter" @mouseleave="mouse_leave" @click="clicked">

    <span class="co-menu-origin">
        <slot></slot>

        <div class="co-menu-hover-area" />

        <div :class="['co-menu-container', right ? 'co-menu-container-right' : center ? 'co-menu-container-center' : 'co-menu-container-left']">
    
            <transition name="co-menu">
                <div v-show="show"  :class="['co-menu', shadow ? 'co-menu-shadow' : shadowDark ? 'co-menu-shadow-dark' : shadowLight ? 'co-menu-shadow-light' : '']">
                    <div :class="['co-menu-triangle', right ? 'co-menu-triangle-right' : center ? 'co-menu-triangle-center' : 'co-menu-triangle-left' ]" />

                    <div class="co-menu-before">
                        <slot name="before"></slot>
                    </div>

                    <div class="co-menu-content">
                        ...
                        <slot name="content"></slot>
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

        hover: Boolean,

        width: String,
        height: String,

        bg: String,

        shadowLight: Boolean,
        shadow: Boolean,
        shadowDark: Boolean,

        lessRound: Boolean,

        left: Boolean,
        right: Boolean,
        center: Boolean,

    },

    setup ( props ) {

        const to_show = ref(false)
        const show = ref(false)
        const show_clickarea = ref(false)

        const border_radius = computed( () => props.lessRound ? '1.5em' : '3.5em' )

        const menu_left_radius = computed( () => ` 0 ${border_radius.value} ${border_radius.value} ${border_radius.value} ` )
        const menu_right_radius = computed( () => ` ${border_radius.value} 0 ${border_radius.value} ${border_radius.value} ` )
        const menu_center_radius = computed( () => border_radius.value )

        const menu_radius = computed( () => props.right ? menu_right_radius.value : props.center ? menu_center_radius.value : menu_left_radius.value )

        const set_menu = () => {
            return setTimeout( () => {
                show.value = to_show.value
            }, 100)
        }

        const mouse_enter = () => {
            if ( props.hover ) to_show.value = true
        }

        const mouse_leave = () => {
            if ( props.hover ) to_show.value = false
        }

        const clicked = () => {
            if ( !props.hover ) {
                if ( to_show.value || show.value ) {
                    to_show.value = false
                    show_clickarea.value = false
                } else {
                    to_show.value = true
                    show_clickarea.value = true
                }
            }
        }
        
        const clicked_out = () => {
            to_show.value = false
            show.value = false
            show_clickarea.value = false
        }

        watch(to_show, set_menu)

        return {
            show,
            to_show,
            show_clickarea,
            mouse_enter,
            mouse_leave,
            clicked,
            clicked_out,
            border_radius,
            menu_radius,
            set_menu
        //     position
        }

    },
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

    width: v-bind(width);
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
    position: absolute;
    top: -50%;
    left: -50%;
    background: transparent;
    width: 200%;
    height: 150%;
    min-height: 8em;
    padding-bottom: v-bind(height);
    z-index: 0;
}

.co-menu-clickout-area {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}


.co-menu {

    background: v-bind(bg);
    border-radius: v-bind(menu_radius);

    display: block;

    min-height: 8em;
    width: v-bind(width);
    height: v-bind(height);

    position: relative;
    
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