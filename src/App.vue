<template>

<main>

<co-card-examples />

</main>

</template>

<script lang="ts">

import CoCardExamples from './components/examples/co-card.examples.vue'

export default {

    name: 'App',

    components: {
        CoCardExamples,
    }
}

</script>
<style scoped>

main {
    @apply w-9/12 m-auto;
}

</style>