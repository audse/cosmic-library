<template>
    
<section class="container">

    <!-- Tab Labels -->
    <nav :class="['labels']">
        <label v-for="tab in tabs" :key="`label-${tab}`" :class="[tab===current_tab ? 'label-active' : '']" @click="current_tab=tab" @keyup.enter="current_tab=tab" tabindex="0">
            <span :for="`Tab ${tab}`"><slot :name="`label-${tab}`"></slot></span>
        </label>
    </nav>

    <!-- Tab Panel -->
    <main :class="[shadow ? 'shadow' : shadowLight ? 'shadow-light' : shadowDark ? 'shadow-dark' : '']">
        
        <section v-for="tab in tabs" :key="`panel-${tab}`">
            <section v-show="current_tab===tab" class="panel">
                <slot :name="`panel-${tab}`"></slot>
            </section>
        </section>

    </main>

</section>

</template>

<script>
import { defineComponent, ref, reactive } from 'vue'

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
    },

    setup ( props ) {

        const class_list = reactive( props.classes ? props.classes : {} )

        const border_radius = props.lessRound ? '1.5em' : '3.5em'

        const current_tab = ref(props.startTab ? props.startTab : 1)

        return {
            class_list,
            border_radius,
            current_tab
        }
        
    },
})

</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
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
}

label {

    position: relative;
    cursor: pointer;

    width: 100%;
    min-height: calc( v-bind(border_radius) + 0.5em );
    border-radius: v-bind(border_radius) v-bind(border_radius) 0 0;
    box-sizing: border-box;
    display: flex;
    justify-content: center;

    padding: 1em 0 calc( v-bind(border_radius) + 0.5em ) 0;

    margin-left: calc( ( v-bind(border_radius) - 0.5em ) * -1 );
    transition: 150ms;
    margin-top: 5px;
    z-index: 1;

    &:first-of-type {
        margin-left: 0;
    }

    span {
        cursor: pointer;
        opacity: 0.75;

    }

    &:hover {
        opacity: 0.75;
        transition: 150ms;
    }

}

.label-active {
    background: v-bind(bg);
    opacity: 1;
    z-index: 2;
    width: 120%;

    span {
        opacity: 1;
    }

    &:hover {
        opacity: 1;
        transition: 150ms;
        margin-top: 0px;
    }
}

main {
    background: v-bind(bg);
    border-radius: v-bind(border_radius);
    margin-top: calc( -1 * v-bind(border_radius) );
    min-height: 8em;
    z-index: 10;
}

section.panel {
    padding: v-bind(border_radius) 1.5em;
    z-index: 10;

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

</style>