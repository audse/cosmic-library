<template>

<div class="space-below">
    <co-title h3 subtitle="co-menus are a container for drop-down content." :classes="classes">
        <co-badge left="<" content="co-menu" right=" />" :color="emphasis" />
        co-menu <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block">

    <div class="flex">

        <co-menu :bg="darkgrey" left hover shadow-dark viewport-width max-width="40vw" :cols="3" :classes="{ before: 'co-bg-lightemphasis co-padding' }">
            <co-button label="Hover Over Me!" :color="emphasis" outline lg />
            <template #toolbar>
                <div class="flex-align-center">
                    <co-button label="!" round :color="emphasis" filled />
                    <co-title h5 title="Toolbar Left" overline="co-menu" :classes="classes" inline />
                </div>
            </template>
            <template #toolbar-right>
                <co-button label="toolbar-right" :color="emphasis" light sm :text-color="truewhite" />
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

        <co-menu bg="rgba(0,0,0,0.6)" center shadow-dark max-width="400px" viewport-width start-open :classes="{ menu: 'co-glass', before: 'co-center co-padding' }">
            <co-button label="Click To Close!" :color="emphasis" subtle lg />
            <template v-slot:before="{ co_menu }">
                <co-title h4 title="Are you sure?" subtitle="Are you sure you want to do that action?" overline="Example" :classes="classes" />
                <div class="co-padding">
                    <co-button label="No, take me back" :color="emphasis" subtle  @click="co_menu.clicked_out()" />
                    <co-button label="Yes, continue" :color="emphasis" :textcolor="truewhite" filled />
                </div>
            </template>
        </co-menu>

    </div>
    <div class="flex flex-right">

        <co-menu :bg="darkgrey" right shadow-dark max-width="40vw" viewport-width>
            <co-button label="Click On Me!" :color="emphasis" :text-color="truewhite" filled lg />
            <template #toolbar-right>
                <co-badge content="Important" :color="emphasis" uppercase />
            </template>
            <template #header>
                <co-title h5 title="Nested Elements" subtitle="any element can be nested within co-menus." overline="info" :classes="classes" />  
            </template>
        </co-menu>
    </div>

</div>
<co-card />

<co-textblock class="co-text-tint-1 space-above">

<co-title h5 title="Slots" overline="co-menu" subtitle="all slots (except the default) are optional." side :classes="classes" />

<div class="textblock space-above">
    <co-badge left="#" content="default"  /> 
    The default slot is the origin. This is the event handler for your menu. Anything added to this slot will open a menu upon click/hover.
</div>

<div class="block space-above">
    <co-badge left="#" content="toolbar" :color="white" /><co-badge left="#" content="toolbar-right" :color="white" />
</div>

<div class="block space-above">
    <co-badge left="#" content="before" :color="white" />
</div>

<div class="block space-above">
    <co-badge left="#" content="content" :color="white" />
</div>

<div class="block space-above">
    <co-badge left="#" content="col-n" :color="white" />
    <co-badge left="#" content="col-1" :color="grey" />
    <co-badge left="#" content="col-2" :color="grey" />
    <co-badge content="etc" :color="grey" />
    Based on the integer set in the 
    <co-badge content="cols" :color="grey" /> prop
</div>

<div class="space-below" />

<co-title h5 title="Scoped Slots" overline="co-menu" subtitle="all slots (except the default) have an optional scope." side :classes="classes" />

<div class="textblock space-above">
    <co-badge content="co_menu" :color="emphasis" />
    <co-badge left="co_menu." content="show_menu()" :color="white" />
    <co-badge left="co_menu." content="mouse_enter()" :color="white" />
    <co-badge left="co_menu." content="mouse_leave()" :color="white" />
    <co-badge left="co_menu." content="clicked()" :color="white" />
    <co-badge left="co_menu." content="clicked_out()" :color="white" />
</div>


<co-title h5 title="Props" overline="co-menu" subtitle="not all the props are optional." side :classes="classes" />

<co-title h6 title="Required Props" :classes="classes" />

<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="viewport-width" :color="white" />
    or
    <co-badge content="string" :color="emphasis" />
    <co-badge content="width" :color="white" />
</div>
<div class="textblock">
    Either set a specific width (in <co-badge content="px" />/<co-badge content="vw" />) or use the boolean <co-badge content="viewport-width" /> to automatically define the width to the size of the screen.
</div>
<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="left" :color="white" />
    or
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="center" :color="white" />
    or
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="right" :color="white" />
</div>
<div class="textblock">
    This defines the location of the menu arrow.    
</div>

<co-title h6 title="All Props" :classes="classes" class="space-above" />

<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="viewport-width" :color="white" />
</div>
<div class="textblock">
    <co-badge content="string" :color="emphasis" />
    <co-badge content="width" :color="white" />
</div>
<div class="textblock">
    <co-badge content="string" :color="emphasis" />
    <co-badge content="max-width" :color="white" /> In <co-badge content="px" /> or <co-badge content="vw" />
</div>
<div class="textblock">
    <co-badge content="string" :color="emphasis" />
    <co-badge content="height" :color="white" />
</div>

<div class="textblock space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="left" :color="white" />
    <co-badge content="right" :color="white" />
    <co-badge content="center" :color="white" />
</div>

<div class="textblock space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="hover" :color="white" />
</div>

<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="reduce-hover-area" :color="white" />
</div>

<div class="textblock space-above">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="start-open" :color="white" />
</div>

<div class="textblock space-above">
    <co-badge content="int" :color="emphasis" />
    <co-badge content="cols" :color="white" />
</div>

<div class="textblock">
    <co-badge content="string" :color="emphasis" />
    <co-badge content="bg" :color="white" />
</div>

<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="shadow" :color="white" />
    <co-badge content="shadow-light" :color="white" />
    <co-badge content="shadow-dark" :color="white" />

    choose <co-badge content="shadow-light" :color="grey" sm /> for light backgrounds, or <co-badge content="shadow-dark" :color="grey" sm /> for dark backgrounds.
</div>
<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="less-round" :color="white" />
</div>
<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="no-col-padding" :color="white" />
</div>
<div class="textblock">
    <co-badge content="boolean" :color="emphasis" />
    <co-badge content="no-arrow" :color="white" />
</div>


<div class="space-above" />

<co-title h5 title="Class Object" overline="co-menu" :classes="classes" />

<div class="space-above" />

<co-title h5 title="Emits" overline="co-menu" :classes="classes" />

<div class="textblock">
    <co-badge content="co-menu-close" right="no props" :color="white" />
</div>

</co-textblock>


</template>

<script>

import { defineComponent } from 'vue'

import LoremIpsum from 'vue-lorem-ipsum'

import CoTitle from './../co-title'
import CoButton from './../co-button'
import CoBadge from './../co-badge'
import CoMenu from './../co-menu'
import CoTextblock from './../co-textblock'
import CoCard from './../co-card'

export default defineComponent({
    
    name: 'co-card-examples',

    components: {
        LoremIpsum,
        CoTitle,
        CoButton,
        CoBadge,
        CoMenu,
        CoTextblock,
        CoCard
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