<template>

<examples component="co-menu" subtitle="co-menus are a container for drop-down content.">
    
    <!-- Examples -->
    <div class="flex-align-center">
        <div class="flex">

            <co-menu :bg="darkgrey" :z-index="1000" left hover shadow-dark viewport-width max-width="900px" :cols="3" :classes="{ before: 'co-bg-lightemphasis co-padding' }">
                <co-button label="Hover Over Me!" :color="emphasis" outline lg />
                <template #toolbar>
                    <div class="flex-align-center">
                        <co-button label="!" round :color="emphasis" filled />
                        <co-title h5 title="Toolbar Left" overline="co-menu" :classes="classes" inline />
                    </div>
                </template>
                <template #toolbar-right>
                    <co-button label="toolbar-right" :color="emphasis" light sm :label-color="truewhite" />
                </template>
                <template #before>
                    <co-badge content="Before" :color="emphasis" />
                </template>
                <template #col-1>
                    <co-title h6 title="Column 1" subtitle="First Column" overline="col-1" :classes="classes" />
                    <LoremIpsum add="5w" />
                </template>
                <template #col-2>
                    <co-title h6 title="Column 2" subtitle="Second Column" overline="col-2" :classes="classes" />
                    <LoremIpsum add="5w" />
                </template>
                <template #col-3>
                    <co-title h6 title="Column 3" subtitle="Third Column" overline="col-3" :classes="classes" />
                    <LoremIpsum add="5w" />
                </template>
            </co-menu>

        </div>
        <div class="flex flex-center">

            <co-menu bg="rgba(0,0,0,0.5)" arrow-overlap="2px" center shadow-dark max-width="400px" viewport-width :classes="{ menu: 'co-glass-light', before: 'co-center co-padding' }">
                <co-button label="Click To Close!" :color="emphasis" subtle lg />
                <template v-slot:before="{ coMenu }">
                    <co-title h4 title="Are you sure?" subtitle="Are you sure you want to do that action?" overline="Example" :classes="classes" />
                    <div class="co-padding">
                        <co-button label="No, take me back" :color="emphasis" subtle  @click="coMenu.clicked_out()" />
                        <co-button label="Yes, continue" :color="emphasis" :textcolor="truewhite" filled />
                    </div>
                </template>
            </co-menu>

        </div>
        <div class="flex flex-right">

            <co-menu :bg="darkgrey" right shadow-dark max-width="300px" viewport-width>
                <co-button label="Click On Me!" :color="emphasis" :label-color="truewhite" filled lg />
                <template #toolbar-right>
                    <co-badge content="Important" :color="emphasis" uppercase />
                </template>
                <template #header>
                    <co-title h5 title="Nested Elements" subtitle="any element can be nested within co-menus." overline="info" :classes="classes" />  
                </template>
            </co-menu>
        </div>

    </div>

    <!-- Slots -->
    <template #slots>
        <p>
            <co-badge left="#" content="default"  /> 
            The default slot is the origin. This is the event handler for your menu. Anything added to this slot will open a menu upon click/hover.
        </p>

        <p>
            <co-badge left="#" content="toolbar" :color="white" />
            <co-badge left="#" content="toolbar-right" :color="white" />
        </p>

        <p><co-badge left="#" content="before" :color="white" /></p>

        <p><co-badge left="#" content="content" :color="white" /></p>

        <p>
            <co-badge left="#" content="col-n" :color="white" />
            <co-badge left="#" content="col-1" :color="grey" />
            <co-badge left="#" content="col-2" :color="grey" />
            <co-badge content="etc" :color="grey" />
            Based on the integer set in the 
            <co-badge content="cols" :color="grey" /> prop
        </p>

        <div class="space-below" />
    </template>

    <!-- Scoped Slots -->
    <template #scoped>

        <p>
            <co-badge content="coMenu" :color="emphasis" />
            <co-badge left="coMenu." content="show_menu()" :color="white" />
            <co-badge left="coMenu." content="mouse_enter()" :color="white" />
            <co-badge left="coMenu." content="mouse_leave()" :color="white" />
            <co-badge left="coMenu." content="clicked()" :color="white" />
            <co-badge left="coMenu." content="clicked_out()" :color="white" />
        </p>

    </template>

    <!-- Props -->
    <template #props>

        <co-title h6 title="Required Props" :classes="classes" />

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="viewport-width" :color="white" />
            or
            <co-badge content="string" :color="emphasis" />
            <co-badge content="width" :color="white" />
            
            Either set a specific width (in <co-badge content="px" />/<co-badge content="vw" />) or use the boolean <co-badge content="viewport-width" /> to automatically define the width to the size of the screen.
        </p>
        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="left" :color="white" />
            or
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="center" :color="white" />
            or
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="right" :color="white" />

            This defines the location of the menu arrow.    
        </p>

        <p>
            <co-badge content="string" :color="emphasis" />
            <co-badge content="arrow-overlap" :color="white" />

            This defines how much the arrow overlaps the body of the menu- useful when using a border. Submit a value + unit such as <co-badge content="2px" />
        </p>

        <co-title h6 title="All Props" :classes="classes" class="space-above" />

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="viewport-width" :color="white" />
        </p>
        <p>
            <co-badge content="string" :color="emphasis" />
            <co-badge content="width" :color="white" />
        </p>
        <p>
            <co-badge content="string" :color="emphasis" />
            <co-badge content="max-width" :color="white" /> In <co-badge content="px" /> or <co-badge content="vw" />
        </p>
        <p>
            <co-badge content="string" :color="emphasis" />
            <co-badge content="height" :color="white" />
        </p>
        <p>
            <co-badge content="int" :color="emphasis" />
            <co-badge content="z-index" :color="white" />

            The default <co-badge content="z-index" /> is 1000: change this if your layout needs something else.
        </p>
        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="left" :color="white" />
            <co-badge content="right" :color="white" />
            <co-badge content="center" :color="white" />
        </p>

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="hover" :color="white" />
        </p>

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="reduce-hover-area" :color="white" />
        </p>

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="start-open" :color="white" />
        </p>

        <p>
            <co-badge content="int" :color="emphasis" />
            <co-badge content="cols" :color="white" />
        </p>

        <p>
            <co-badge content="string" :color="emphasis" />
            <co-badge content="bg" :color="white" />
        </p>

        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="shadow" :color="white" />
            <co-badge content="shadow-light" :color="white" />
            <co-badge content="shadow-dark" :color="white" />

            choose <co-badge content="shadow-light" :color="grey" sm /> for light backgrounds, or <co-badge content="shadow-dark" :color="grey" sm /> for dark backgrounds.
        </p>
        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="less-round" :color="white" />
        </p>
        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="no-col-padding" :color="white" />
        </p>
        <p>
            <co-badge content="boolean" :color="emphasis" />
            <co-badge content="no-arrow" :color="white" />
        </p>
    </template>

    <!-- Emits -->
    <template #emits>
        <p>
            <co-badge content="coMenuOpened" right="no props" :color="white" />
        </p>
        <p>
            <co-badge content="coMenuClosed" right="no props" :color="white" />
        </p>
    </template>

</examples>

</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import Examples from './examples'
import CoTitle from './../co-title'
import CoButton from './../co-button'
import CoBadge from './../co-badge'
import CoMenu from './../co-menu'

export default defineComponent({
    
    name: 'co-card-examples',

    components: {
        LoremIpsum,

        Examples,

        CoTitle,
        CoButton,
        CoBadge,
        CoMenu,
    },

   setup () {

        const emphasis = '#da4790'
        const emphasis_light = '#ee96c2'
        const truewhite = '#ffffff'
        const white = '#a9b6c5'
        const grey = '#7d8894'
        const darkgrey = '#303542'
        const darkbg = '#1d212b'

        const classes = {
            subtitle: 'co-text-tint-2',
            overline: 'co-text-emphasis'
        }

        return {
            emphasis,
            emphasis_light,
            truewhite,
            white,
            grey,
            darkgrey,
            darkbg,
            classes
        }
    }

})

</script>

<style scoped>

.top-of-stack {
    z-index: 100;
}

</style>