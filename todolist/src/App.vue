<template>
    <div id="app">
        <input type="text" ref="txt" class="txtb" v-model="msg" @keydown="enterDown">&nbsp;
        <button class="btn" @click="daADD">确定</button>
        <ul>
            <div class="notcomp">
                <h3>Not Completed</h3>
                <li v-for="(item,key) in list" class="task" v-if="!item.flag">
                    <input type="checkbox" v-model="item.flag" @change="saveList"> {{item.title}} <i class='fa fa-trash' @click="deleteData(key)"></i>
                    <!--{{item.title}} <i class='fa fa-trash' @click="deleteData(key)"></i> <i class='fa fa-check' @click="saveList"></i> <button @click="deleteData(key)">删除</button>-->
                </li>
            </div>
            <div class="comp">
                <h3>Completed</h3>
                <li v-for="(item,key) in list" class="task" v-if="item.flag">
                    <input type="checkbox" v-model="item.flag" @change="saveList"> {{item.title}} <i class='fa fa-trash' @click="deleteData(key)"></i>
                    <!--{{item.title}} <i @click="deleteData(key)" class='fa fa-trash'></i> <button @click="deleteData(key)">删除</button>-->
                </li>
            </div>
        </ul>
    </div>
</template>

<script>
    import storage from './model/storage.js';
    // console.log(storage);
    export default {
        data() {
            return {
                msg:'',
                list:[],
            }
        },
        methods:{
            enterDown(e){
                if (e.keyCode === 13 && this.$refs.txt.value !== ""){
                    this.list.push({
                        title:this.msg,
                        flag:false,
                    });
                    this.msg = '';
                }
                // localStorage.setItem('list',JSON.stringify(this.list));
                storage.set('list',this.list);
            },
            daADD(){
                if (this.$refs.txt.value !== "") {
                    this.list.push({
                        title:this.msg,
                        flag:false,
                    });
                    this.msg = '';
                    // localStorage.setItem('list',JSON.stringify(this.list));
                    storage.set('list',this.list);
                }
            },
            deleteData(key){
                this.list.splice(key,1);
                // localStorage.setItem('list',JSON.stringify(this.list));
                storage.set('list',this.list);
            },
            saveList(){
                // localStorage.setItem('list',JSON.stringify(this.list));
                storage.set('list',this.list);
            },
        },
        mounted(){/*生命周期 vue刷新界面运行*/
            // var list = JSON.parse(localStorage.getItem('list'));
            var list = storage.get('list');
            if (list){
                this.list = list;
            }
        },
    }
</script>

<style>
    *{
        margin: 0;
        padding: 0;
        font-family: "montserrat",sans-serif;
        box-sizing: border-box;
    }

    body{
        background-image: linear-gradient(120deg,#487eb0,#fbc531);
        min-height: 100vh;
    }

    #app{
        max-width: 800px;
        margin: auto;
        padding: 10px;
    }

    .txtb{
        width: 85%;
        border: none;
        border-bottom: 2px solid #000;
        background: none;
        padding: 10px;
        margin-left: 3px;
        outline: none;
        font-size: 18px;
    }

    h3{
        margin: 10px 0;
    }

    .task{
        width: 100%;
        background: rgba(225,225,225,0.5);
        padding: 18px;
        margin: 6px 0;
        overflow: hidden;
    }

    .task i{
        float: right;
        margin-left: 20px;
        cursor: pointer;
    }

    .comp .task{
        background: rgba(0,0,0,.5);
        color: #fff;
    }
    ul{
        list-style: none;
    }
    .btn{
        width: 12%;
        background: #2c3e50;
        border: 0;
        color: white;
        padding: 10px 0;
        border-radius: 6px;
        cursor: pointer;
    }
</style>

