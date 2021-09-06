<template>
    
<div :class="['co-tabs-container']">

    <!-- Tab Labels -->
    <div :class="['co-tabs-labels']">
        <div v-for="tab in tabs" :key="`co-tabs-label-${tab}`" :class="['co-tabs-label', tab===current_tab ? 'co-tabs-label-active' : '']" @click="current_tab=tab">
            <label :for="`Tab ${tab}`"><slot :name="`tab-label-${tab}`"></slot></label>
        </div>
    </div>

    <!-- Tab Panel -->
    <div :class="['co-tabs-panels', shadow ? 'co-tabs-shadow' : shadowLight ? 'co-tabs-shadow-light' : shadowDark ? 'co-tabs-shadow-dark' : '']">
        
            <transition-group name="co-tab-panel" mode="out-in">
                <div>
                    <div v-for="tab in tabs" :key="`co-tabs-panel-${tab}`">
                        <div v-if="current_tab===tab">
                            <div class="co-tab-panel-before">
                                <slot :name="`tab-panel-${tab}-before`"></slot>
                            </div>
                            <div class="co-tab-panel">
                                <slot :name="`tab-panel-${tab}`"></slot>
                            </div>
                        </div>
                    </div>
                </div>
        </transition-group>
    </div>

</div>

</template>

<script>
import { defineComponent, computed, ref } from 'vue'

export default defineComponent({

    name: 'co-tabs',

    props: {
        tabs: Number,
        startTab: Number,

        classes: Object,

        bg: String,

        inactiveColor: String,

        shadow: Boolean,
        shadowLight: Boolean,
        shadowDark: Boolean,
        lessRound: Boolean,
    },

    setup ( props ) {

        const class_list = computed( () => props.classes ? props.classes : {} )

        const border_radius = props.lessRound ? '1em' : '2em'
        const inactive_color = computed( () => props.inactiveColor ? props.inactiveColor : props.bg )

        const current_tab = ref(props.startTab ? props.startTab : 1)

        return {
            class_list,
            border_radius,
            inactive_color,

            current_tab
        }
        
    },
})

</script>

<style lang="scss" scoped>

.co-tabs-container {

    width: 100%;
    overflow-x: hidden;

}

.co-tabs-labels {
    display: flex;
    margin-left: calc( v-bind(border_radius) + 0.5em );
    max-width: calc( 100% - ( ( v-bind(border_radius) * 2 ) + 1em ) );
}

.co-tabs-label {

    background: v-bind(inactive_color);
    border-radius: 1.5em 1.5em 0 0;
    padding: 1em 2em 0.5em 2em;
    position: relative;
    margin-left: -1.75em;
    cursor: pointer;

    &:first-of-type {
        margin-left: 0;
    }

    label {
        opacity: 0.75;
    }

    &:hover {
        opacity: 0.75;
        transition: 200ms;
        margin-top: -1px;
    }

}

.co-tabs-label-active {
    background: v-bind(bg);
    opacity: 1;
    z-index: 2;
    padding: 1em 2.25em 0.5em 2.25em;
    top: 0px;

    label {
        opacity: 1;
    }

    &:hover {
        opacity: 1;
    }
}

.co-tabs-panels {
    background: v-bind(bg);
    border-radius: v-bind(border_radius);
    min-height: 8em;
}

.co-tab-panel-before {

}

.co-tab-panel {
    padding: 2.5em 1.5em;
}

.co-tab-panel-enter-active {
    transform: translateX(100%);
    transition: 350ms;
}

.co-tab-panel-enter-to {
    transform: translateX(0%);
    transition: 350ms;
}

.co-tab-panel-leave-active {
    transform: translateX(-100%);
    transition: 350ms;
}

.co-tab-panel-leave-from {
    transform: translateX(0%);
    transition: 350ms;
}

.co-tabs-label:before,
.co-tabs-label:after {
    z-index: -1;
    content: "";
    position: absolute;

    height: 12px;
    width: 24px;

    bottom: 0;
    transition: 200ms;
}

.co-tabs-label:after {
    right: -24px;

    border-radius: 0 0 0 12px;
    -moz-border-radius: 0 0 0 12px;
    -webkit-border-radius: 0 0 0 12px;

    -webkit-box-shadow: -12px 0 0 0 v-bind(inactive_color);
    box-shadow: -12px 0 0 0 v-bind(inactive_color);
}

.co-tabs-label:before {
    left: -24px;

    border-radius: 0 0 12px 0;
    -moz-border-radius: 0 0 12px 0;
    -webkit-border-radius: 0 0 12px 0;

    -webkit-box-shadow: 12px 0 0 0 v-bind(inactive_color);
    box-shadow: 12px 0 0 0 v-bind(inactive_color);
}

.co-tabs-label-active:after {
    right: -24px;

    border-radius: 0 0 0 12px;
    -moz-border-radius: 0 0 0 12px;
    -webkit-border-radius: 0 0 0 12px;

    -webkit-box-shadow: -12px 0 0 0 v-bind(bg);
    box-shadow: -12px 0 0 0 v-bind(bg);
}

.co-tabs-label-active:before {
    left: -24px;

    border-radius: 0 0 12px 0;
    -moz-border-radius: 0 0 12px 0;
    -webkit-border-radius: 0 0 12px 0;

    -webkit-box-shadow: 12px 0 0 0 v-bind(bg);
    box-shadow: 12px 0 0 0 v-bind(bg);
}


.co-tabs-shadow-light {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.15);
}

.co-tabs-shadow {
    box-shadow: 0px 5px 25px -20px rgba(0, 0, 0, 0.4);
}

.co-tabs-shadow-dark {
    box-shadow: 0px 10px 30px -20px rgba(0, 0, 0, 0.7);
}

</style>