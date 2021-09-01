<template>

<div id="container">

    <HomePage />

</div>

</template>

<script>
import HomePage from './pages/Home.page'

export default {

    name: 'App',

    components: {
        HomePage
    }
}
</script>

<style>

body {
    background: #e7ebeb;

    --co-color-text: #363333;
    --co-color-background: #fdfdfd;

}

* {
    font-family: 'Fira Sans', sans-serif;
    font-size: 16px;
}

#container {
    display: flex;
    margin: 0 auto;
    width: 768px;
}

.pink {
    color: hotpink;
}

</style>
