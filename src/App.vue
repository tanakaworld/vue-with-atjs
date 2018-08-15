<template>
    <div id="app">
        <h1>WYSIWYG Editor (Vue + At.js)</h1>
        <WYSIWYG v-model="wysiwygContent"/>
        <pre class="debug">{{wysiwygContent}}</pre>
    </div>
</template>

<script>
    import WYSIWYG from './components/WYSIWYG';

    export default {
        name: 'app',
        components: {
            WYSIWYG
        },
        data() {
            return {
                wysiwygContent: ''
            };
        }
    };
</script>

<style>
    :root {
        --color-white: #FFFFFF;
        --color-gray: #dddddd;
        --color-black: #333333;
        --color-green: #62B587;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .debug {
        text-align: left;
        background-color: var(--color-gray);
        padding: 12px;
        white-space: pre-line;
    }
</style>
