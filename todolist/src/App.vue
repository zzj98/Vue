<template>
    <div id="app">
        <input type="text" v-model="msg">&nbsp;
        <button @click="daADD">确定</button>
        <hr/>
        <ul>
            <h3>正在进行的事件</h3>
            <li v-for="(item,key) in list" v-if="!list.flag">
                <input type="checkbox" v-model="list.flag"> {{item.title}} <button @click="deleteData(key)">删除</button>
            </li>
            <h3>已完成的事件</h3>
            <li v-for="(item,key) in list" v-if="list.flag">
                <input type="checkbox" v-model="list.flag"> {{item.title}} <button @click="deleteData(key)">删除</button>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                msg:'',
                list:[],
            }
        },
        methods:{
            daADD(){
                this.list.push({
                    title:this.msg,
                    flag:false,
                });
                this.msg = '';
            },
        }
    }
</script>

<style>
    ul{
        list-style: none;
    }
</style>

