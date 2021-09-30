<script lang="ts" setup>

import CoCardExamples from './components/examples/co-card.examples.vue'
import CoListExamples from './components/examples/co-list.examples.vue'
import CoTabsExamples from './components/examples/co-tabs.examples.vue'
import CoMenuExamples from './components/examples/co-menu.examples.vue'
import CoTextInputExamples from './components/examples/co-textinput.examples.vue'


</script>
<template>

<main>

<co-text-input-examples />
<co-menu-examples />
<co-tabs-examples />
<co-list-examples />
<co-card-examples />

</main>

</template>

<script lang="ts">

export default {
    name: 'App'
}

</script>
<style scoped>

main {
    @apply w-9/12 m-auto;
}

</style>