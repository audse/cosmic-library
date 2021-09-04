<template>

<div class="space-below">
    <co-title h3 subtitle="co-menus are a container for drop-down content." :classes="classes">
        <co-badge left="<" content="co-menu" right=" />" :color="emphasis" />
        co-menu <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block">

    <div class="flex">

        <co-menu :bg="grey" left shadow-dark hover viewport-width max-width="40vw">
            <co-button label="Hover Over Me!" :color="emphasis" outline lg />
        </co-menu>

    </div>
    <div class="flex flex-right">

        <co-menu :bg="grey" right shadow-dark max-width="40vw" viewport-width>
            <co-button label="Click On Me!" :color="emphasis" :text-color="truewhite" filled  lg/>
        </co-menu>
    </div>

</div>

</template>

<script>

import { defineComponent } from 'vue'

// import LoremIpsum from 'vue-lorem-ipsum'

import CoTitle from './../co-title'
import CoButton from './../co-button'
import CoBadge from './../co-badge'
import CoMenu from './../co-menu'

export default defineComponent({
    
    name: 'co-card-examples',

    components: {
        // LoremIpsum,
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
        const grey = '#303542'

        const classes = {
            subtitle: 'co-text-tint-2'
        }

        return {
            emphasis,
            emphasis_light,
            truewhite,
            white,
            grey,
            classes
        }
    }

})

</script>
<style lang="scss" scoped>

.space-above {
    padding-top: 1.5em;
}

.block {
    margin: 0.5em 0;
    display: flex;
    align-items: center;
}

.menu-block {
    flex: 1 auto;
    position: relative;
}

</style>