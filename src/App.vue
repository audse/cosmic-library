<template>

<div id="wrapper">

    <Sidebar />
    <HomePage />

</div>

</template>

<script>
import Sidebar from './layouts/Sidebar'
import HomePage from './layouts/Home.page'

export default {

    name: 'App',

    components: {
        Sidebar,
        HomePage
    }
}
</script>
