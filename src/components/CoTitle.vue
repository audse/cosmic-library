<template>

<div :class="['co-title', class_list.title_group]">
    <div :class="['co-title-title', class_list.title]">

        <div :class="['co-title-overline', class_list.overline]">
            {{ overline }}
            <slot name="overline"></slot>
        </div>

        {{ title }}

        <slot name="title"></slot>
    </div>
    <div :class="['co-title-subtitle', class_list.subtitle]">
        {{ subtitle }}
        <slot name="subtitle"></slot>
    </div>
</div>

</template>
<script>
import { defineComponent, computed } from 'vue'

export default defineComponent({

    name: 'CoTitle',

    props: {
        title: String,
        subtitle: String,
        overline: String,

        classes: Object,
    },

    setup ( props ) {
        
        const class_list = computed( () => props.classes ? Object.assign({}, props.classes) : {} )

        return {
            class_list
        }
    }


})
</script>
<style scoped>

.co-title-overline {

    font-size: 0.7em;
    letter-spacing: 1px;
    text-transform: uppercase;
    
}

.co-title-title {

    font-size: 1.25em;
    font-weight: 600;
    line-height: 1.2;

    padding: 1em 0.75em 0.25em 0.75em;
}

.co-title-subtitle {

    opacity: 0.5;
    
    font-size: 1.1em;
    line-height: 1.3;

    padding: 0.25em 0.75em;

}

</style>