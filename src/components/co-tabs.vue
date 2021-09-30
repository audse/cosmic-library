<template>
    
<section :class="['container', classList.container]">

    <!-- Tab Labels -->
    <nav :class="['labels']">
        <label v-for="tab in tabs" :key="`label-${tab}`" :class="[tab===currentTab ? 'label-active' : '', classList.label]" @click="currentTab=tab" @keyup.enter="currentTab=tab" tabindex="0" :for="`Tab ${tab}`">
            <slot :name="`label-${tab}`"></slot>
        </label>
    </nav>

    <!-- Tab Panel -->
    <article :class="[shadow ? 'shadow' : shadowLight ? 'shadow-light' : shadowDark ? 'shadow-dark' : '']">
        
        <transition name="slide" mode="out-in">

            <section :class="['panel', noPadding ? '' : 'panel-padding', classList.panel]" :key="`panel-${currentTab}`">
                <slot :name="`panel-${currentTab}`"></slot>
            </section>

        </transition>
    </article>

</section>

</template>

<script>
import { defineComponent, ref, reactive, watch } from 'vue'

export default defineComponent({

    name: 'co-tabs',

    props: {
        tabs: Number,
        startTab: Number,

        classes: Object,

        bg: String,

        shadow: Boolean,
        shadowLight: Boolean,
        shadowDark: Boolean,
        lessRound: Boolean,
        noPadding: Boolean,
    },

    setup ( props ) {

        const classList = reactive( props.classes ? props.classes : {} )

        const borderRadius = props.lessRound ? '1.5em' : '3.5em'

        const currentTab = ref(props.startTab ? props.startTab : 1)

        return {
            classList,
            borderRadius,
            currentTab,
        }
        
    },
})

</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
    display: block;
    position: relative;
    padding: 0;
    margin: 0;
}

section.container {

    width: 100%;
    flex: none;
    display: block;
    overflow-x: hidden;
    position: relative;
    isolation: isolate;

    margin: 0;
    padding: 0;

}

nav {
    display: flex;
    justify-content: center;
    z-index: 1;
    width: 100%;
}

label {

    position: relative;
    cursor: pointer;

    flex: 1 auto;
    flex-basis: calc( 100% / v-bind(tabs) );

    min-height: calc( v-bind(borderRadius) + 0.5em );
    border-radius: v-bind(borderRadius) v-bind(borderRadius) 0 0;
    box-sizing: border-box;
    display: flex;
    justify-content: center;

    padding: 1em 0 calc( v-bind(borderRadius) + 0.5em ) 0;

    transition: 150ms;
    margin-top: 5px;
    z-index: 1;

    outline: none;

    &:first-of-type {
        margin-left: 0;
    }

    span {
        cursor: pointer;
        opacity: 0.75;

    }

    &:hover {
        opacity: 0.75;
        transition: all 150ms;
    }

}

.label-active {
    background: v-bind(bg);
    opacity: 1;
    z-index: 2;
    
    flex-basis: calc( ( 100% / v-bind(tabs) ) + 10% );

    span {
        opacity: 1;
    }

    &:hover {
        opacity: 1;
        transition: all 150ms;
        margin-top: 0px;
    }
}

article {
    background: v-bind(bg);
    border-radius: v-bind(borderRadius);
    margin-top: calc( -1 * v-bind(borderRadius) );
    min-height: 8em;
    z-index: 10;
}

section.panel {
    z-index: 10;

}

section.panel-padding {
    padding: v-bind(borderRadius) 1.5em;
}

.shadow-light {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.15);
}

.shadow {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.4);
}

.shadow-dark {
    box-shadow: 0px 10px 30px -20px rgba(0, 0, 0, 0.7);
}

.slide-enter-from {
    transform: scaleY(0.9) translateX(33%);
    opacity: 0;
}

.slide-enter-to {
    transform: scaleY(1) translateX(0%);
    opacity: 1;
}

.slide-leave-from {
    transform: scaleY(1) translateX(0%);
    opacity: 1;
}

.slide-leave-to {
    transform: scaleY(0.9) translateX(-33%);
    opacity: 0;
}

.slide-enter-active, .slide-leave-active {
    transition: all 250ms;
}

</style>