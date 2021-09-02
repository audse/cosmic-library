
<template>

<p>
    <slot></slot>
</p>    

</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    
    name: 'co-textblock',

    props: {
        classes: String,
    }
})


</script>

<style lang="scss" scoped>

p {
    font-size: 1em;
    line-height: 1.6;
}

</style>