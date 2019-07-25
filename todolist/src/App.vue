<template>
    <div id="app">
        <input type="text" v-model="msg" @keydown="enterDown">&nbsp;
        <button @click="daADD">确定</button>
        <hr/>
        <ul>
            <h3>正在进行的事件</h3>
            <li v-for="(item,key) in list" v-if="!item.flag">
                <input type="checkbox" v-model="item.flag" @change="saveList"> {{item.title}} <button @click="deleteData(key)">删除</button>
            </li>
            <h3>已完成的事件</h3>
            <li v-for="(item,key) in list" v-if="item.flag">
                <input type="checkbox" v-model="item.flag" @change="saveList"> {{item.title}} <button @click="deleteData(key)">删除</button>
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
            enterDown(e){
                if (e.keyCode === 13 ){
                    this.list.push({
                        title:this.msg,
                        flag:false,
                    });
                    this.msg = '';
                }
                localStorage.setItem('list',JSON.stringify(this.list));
            },
            daADD(){
                this.list.push({
                    title:this.msg,
                    flag:false,
                });
                this.msg = '';
                localStorage.setItem('list',JSON.stringify(this.list));
            },
            deleteData(key){
                this.list.splice(key,1);
                localStorage.setItem('list',JSON.stringify(this.list));
            },
            saveList(){
                localStorage.setItem('list',JSON.stringify(this.list));
            },
        },
        mounted(){
            var list = JSON.parse(localStorage.getItem('list'));
            if (list){
                this.list = list;
            }
        },
    }
</script>

<style>
    ul{
        list-style: none;
    }
</style>

