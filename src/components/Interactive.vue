<template>
    <div class="interactive">
        <div class="int-title">
            <h1 class="is-size-5">{{title}}</h1>
        </div>
        <div class="int-caption">
            <p class="is-size-6">{{caption}}</p>
        </div>
        <div class="int-content">
            <DataVisualization></DataVisualization>
        </div>
        <div class="int-source">
            <p class="is-size-7">{{source}}</p>
        </div>
    </div>
</template>

<script>
    /* eslint-disable no-console */


    import DataVisualization from './DataVisualization'

    export default {
        name: 'Interactive',
        components: {
            DataVisualization
        },
        props: {
            title: String,
            caption: String,
            source: String
        },
        mounted: function () {
            console.log("Interactive mounted");
        }
    }
</script>

<style scoped lang="scss">
    .interactive {
        background-color: #ddd; // debug
        max-width: 750px;
        min-height: 365px;
        padding: 10px;
    }

    .int-title {
        h1 {
            font-weight: bold;
        }
    }

    .int-caption {

    }

    .int-content {
        margin: 5px 0;
        background-color: white;
    }

    .int-source {

    }
</style>
