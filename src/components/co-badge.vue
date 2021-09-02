<template>
    
<div :class="['co-badge', classes, uppercase ? 'co-badge-uppercase' : '', large ? 'co-badge-size-lg' : 'co-badge-size-md']">
    {{ content }}
    <slot></slot>
</div>

</template>
<script>

import { defineComponent } from 'vue'

export default defineComponent({

    name: 'CoBadge',

    props: {
        content: String,
        classes: String,

        large: Boolean,
        uppercase: Boolean,
    },

})

</script>

<style scoped>

.co-badge {

    /* Background */
    background: rgba(var(--co-color-emphasis), 0.25);
    border-radius: 1em;

    /* Text */
    letter-spacing: 0.5px;

    /* Positioning */
    display: inline-block;

    /* Spacing */
    margin: 0.25em 0.5em 0.25em 0;
    padding: 0.25em 0.5em 0.1em 0.5em;

    /* Sizing */
    width: fit-content;
}

.co-badge-size-lg {
    font-size: 1em;
}

.co-badge-size-md {
    font-size: 0.75em;
}

.co-badge-uppercase {
    text-transform: uppercase;
}

</style>
