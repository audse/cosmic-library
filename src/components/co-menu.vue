
<template>

<span class="co-menu-group" @mouseenter="show=true" @mouseleave="show=false">

    <span>
        <slot name="handler"></slot>
    </span>

    <transition name="co-menu">
        <div v-show="show"  :class="['co-menu-container']">
            <div :class="['co-menu-triangle']" />
            
            <div :class="['co-menu', shadow ? 'co-menu-shadow' : shadowDark ? 'co-menu-shadow-dark' : shadowLight ? 'co-menu-shadow-light' : '']">
                
                <div class="co-menu-before">
                    <slot name="before"></slot>
                </div>

                <div class="co-menu-content">
                    ...
                    <slot></slot>
                </div>

            </div>
        </div>
    </transition>
</span>

</template>
<script>

import { defineComponent, computed, ref } from 'vue'

export default defineComponent({

    name: 'co-menu',

    props: {
        width: String,
        height: String,

        bg: String,

        shadowLight: Boolean,
        shadow: Boolean,
        shadowDark: Boolean,

        lessRound: Boolean,

        right: Boolean,

    },

    setup ( props ) {

        const show = ref(false)

        const border_radius = computed( () => props.lessRound ? '1.5em' : '3.5em' )

        const menu_left_radius = computed( () => ` 0 ${border_radius.value} ${border_radius.value} ${border_radius.value} ` )
        const menu_right_radius = computed( () => ` ${border_radius.value} 0 ${border_radius.value} ${border_radius.value} ` )

        const menu_radius = computed( () => props.right ? menu_right_radius.value : menu_left_radius.value )

        const triangle_left_width = '0 32px 16px 0px'
        const triangle_right_width = '0 0 16px 32px'
        const triangle_left_color = `transparent transparent ${props.bg} transparent`
        const triangle_right_color = `transparent transparent ${props.bg} transparent`

        const triangle_width = computed( () => props.right ? triangle_right_width : triangle_left_width )
        const triangle_color = computed( () => props.right ? triangle_right_color : triangle_left_color )

        return {
            show,
            border_radius,
            menu_radius,
            triangle_width,
            triangle_color
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

.co-menu-group {
    position: relative;
}

.co-menu-container {

    width: v-bind(width);
    max-width: 100%;
    height: v-bind(height);
    padding: 16px;

    position: absolute;
    left: 25%;
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
    border-width: v-bind(triangle_width);
    border-color: v-bind(triangle_color);

    position: absolute;
    top: 0;
}

.co-menu-enter-active,
.co-menu-leave-active {
    transition: 250ms ease;
}

.co-menu-enter-from,
.co-menu-leave-to {
    transform: translateY(-0.5em);
    transform-origin: -1em -1em;
    opacity: 0;
}

</style>