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
        
        <div v-for="tab in tabs" :key="`co-tabs-panel-${tab}`">
            <div v-show="current_tab===tab">
                <div class="co-tabs-panel-before">
                    <slot :name="`tab-panel-${tab}-before`"></slot>
                </div>
                <div class="co-tabs-panel">
                    <slot :name="`tab-panel-${tab}`"></slot>
                </div>
            </div>
        </div>

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

        const border_radius = props.lessRound ? '1.5em' : '3.5em'
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
    position: relative;
    isolation: isolate;

}

.co-tabs-labels {
    display: flex;
    // max-width: calc( 100% - ( ( v-bind(border_radius) * 2 ) + 1em ) );
    justify-content: center;
    z-index: 1;
}

.co-tabs-label {

    position: relative;
    cursor: pointer;

    width: 100%;
    min-height: calc( v-bind(border_radius) + 0.5em );
    border-radius: v-bind(border_radius) v-bind(border_radius) 0 0;
    box-sizing: border-box;
    display: flex;
    justify-content: center;

    padding: 1em 0 calc( v-bind(border_radius) + 1em ) 0;

    margin-left: calc( ( v-bind(border_radius) * 2 ) * -1 );

    &:first-of-type {
        margin-left: 0;
    }

    label {
        opacity: 0.75;

    }

    &:hover {
        opacity: 0.75;
        transition: 150ms;
        margin-top: -1px;
    }

}

.co-tabs-label-active {
    background: v-bind(bg);
    opacity: 1;
    z-index: 2;

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
    margin-top: calc( -1 * v-bind(border_radius) );
    min-height: 8em;
    z-index: 10;
}

.co-tab-panel-before {

}

.co-tabs-panel {
    padding: v-bind(border_radius) 1.5em;
    z-index: 10;
}


// .co-tabs-label:before,
// .co-tabs-label:after {
//     z-index: -1;
//     content: "";
//     position: absolute;

//     height: 12px;
//     width: 24px;

//     bottom: 0;
//     transition: 200ms;
// }

// .co-tabs-label:after {
//     right: -24px;

//     border-radius: 0 0 0 12px;
//     -moz-border-radius: 0 0 0 12px;
//     -webkit-border-radius: 0 0 0 12px;

//     -webkit-box-shadow: -12px 0 0 0 v-bind(inactive_color);
//     box-shadow: -12px 0 0 0 v-bind(inactive_color);
// }

// .co-tabs-label:before {
//     left: -24px;

//     border-radius: 0 0 12px 0;
//     -moz-border-radius: 0 0 12px 0;
//     -webkit-border-radius: 0 0 12px 0;

//     -webkit-box-shadow: 12px 0 0 0 v-bind(inactive_color);
//     box-shadow: 12px 0 0 0 v-bind(inactive_color);
// }

// .co-tabs-label-active:after {
//     right: -24px;

//     border-radius: 0 0 0 12px;
//     -moz-border-radius: 0 0 0 12px;
//     -webkit-border-radius: 0 0 0 12px;

//     -webkit-box-shadow: -12px 0 0 0 v-bind(bg);
//     box-shadow: -12px 0 0 0 v-bind(bg);
// }

// .co-tabs-label-active:before {
//     left: -24px;

//     border-radius: 0 0 12px 0;
//     -moz-border-radius: 0 0 12px 0;
//     -webkit-border-radius: 0 0 12px 0;

//     -webkit-box-shadow: 12px 0 0 0 v-bind(bg);
//     box-shadow: 12px 0 0 0 v-bind(bg);
// }


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