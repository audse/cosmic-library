<template>

<div class="space-below">
    <co-title h3 subtitle="co-menus are a container for drop-down content." :classes="classes">
        <co-badge left="<" content="co-menu" right=" />" :color="emphasis" />
        co-menu <span class="co-text-tint-1">component</span>
    </co-title>
</div>

<div class="block">

    <co-menu :bg="grey" width="50vw" shadow-dark>
        <template #handler>
            <co-button label="Show Menu" :color="emphasis" subtle />
        </template>
    </co-menu>
    <co-menu :bg="grey" width="10vw" right shadow-dark>
        <template #handler>
            <co-button label="Show Menu" :color="emphasis" subtle />
        </template>
    </co-menu>

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