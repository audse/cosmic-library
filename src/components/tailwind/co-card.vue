<template>
    
<article>

    <section class="top" v-if="this.$slots['header'] || this.$slots['toolbar'] || this.$slots['toolbar-right']">

        <!-- Toolbar -->
        <nav v-if="this.$slots['toolbar'] || this.$slots['toolbar-right']">
            <slot name="toolbar"></slot>
            <aside class="right">
                <slot name="toolbar-right"></slot>
            </aside>
        </nav>

        <!-- Header -->
        <header v-if="this.$slots['header']">
            <slot name="header"></slot>
        </header>

    </section>

    <!-- Main Content -->
    <section v-if="this.$slots['default']">

    </section>

    <section class="bottom">

        <!-- Footer -->
        <footer v-if="this.$slots['footer']">
            <slot name="footer"></slot>
        </footer>

        <!-- Actions -->
        <nav v-if="this.$slots['actions'] || this.$slots['actions-right']">
            <slot name="actions"></slot>
            <aside class="right">
                <slot name="actions-right"></slot>
            </aside>
        </nav>

    </section>

</article>

</template>
<script lang="ts">

export default {
    name: 'co-card',
    props: {
        bg: String,
    }
}

</script>
<style lang="scss" scoped>

article {
    border-radius: 3rem;
    background-color: v-bind(bg);
}

article header, article footer {
    @apply px-4 py-6;
}

article nav {
    @apply px-4 pt-6 pb-1 flex;
}

article nav.right {
    @apply text-right;
}

</style>
