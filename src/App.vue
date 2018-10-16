<template>
    <div id="app">
        <Interactive title="Control gubernamental de la corrupción"
                     caption="Con algunas excepciones, la mayoría de los países de ALC han empeorado su control de la corrupción."
                     source="Fuente: WGI, 2017">
        </Interactive>
    </div>
</template>

<script>
    /* eslint-disable no-console */

    import Interactive from './components/Interactive.vue'

    export default {
        name: 'app',
        components: {
            Interactive
        },
        data: function () {
            return {

            }
        },
        mounted: function () {
            console.log("App mounted");
        },
    }
</script>

<style lang="scss">
    @import url('https://fonts.googleapis.com/css?family=Montserrat:400,700&subset=latin-ext');
    @import '~bulma/bulma';

    #app {
        font-family: 'Montserrat', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }
</style>
