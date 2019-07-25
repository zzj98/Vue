<template>
    <div id="app">
        {{msg}}
        <v-home></v-home>
    </div>
</template>

<script>
    import  Home from './components/Home';/*引入组件*/
    export default {
        data() {
            return {
                msg: '你好vue',
            }
        },
        methods:{        },
        components:{
            'v-home':Home/*挂载组件*/
        }
    }
</script>
