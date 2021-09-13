<template>
    
<li>
    <aside v-if="this.$slots.left" :class="['left', classList.left]">
        <span>
            <slot name="left"></slot>
        </span>
    </aside>

    <section v-if="this.$slots.before" :class="['before', classList.before]">
        <slot name="before"></slot>
    </section>

    <section v-if="this.$slots.default" :class="['content', classList.content]">
        <main>
            <slot></slot>
        </main>
    </section>

    <aside v-if="this.$slots.right" :class="['right', classList.right]">
        <span>
            <slot name="right"></slot>
        </span>
    </aside>
</li>

</template>

<script>

import { defineComponent, reactive } from 'vue'

export default defineComponent({

    name: 'co-list-item',

    props: {
        classes: Object,

        borderColor: String,

        hoverDark: Boolean,
        hoverLight: Boolean,
        hoverColor: String,
    },

    setup ( props ) {
        
        const classList = reactive( props.classes ? props.classes : {} )

        return {
            classList
        }

    },

})

</script>

<style lang="scss" scoped>

* {
    box-sizing: border-box;
    display: block;
    position: relative;
    margin: 0;
    padding: 0;
}

</style>
