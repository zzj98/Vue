<template>
    <div id="app">
        {{msg}}
        <br/><br/>
        <button v-on:click="run1">执行第一种方法</button>
        <button @click="run2">执行第二种方法</button>
        <br/><br/>
        <button @click="getMsg">获取data里msg</button>
        <br/><br/>
        <button @click="setMsg">改变data里msg</button>
        <br/><br/>
        <button @click="requestData">请求数据</button><br/>
        <ul>
            <li v-for="(item,key) in list">
                {{key}}:{{item}}
            </li>
        </ul>
        <br/><br/>
        <button @click="deleteData('111')">执行方法传值</button><br/>
        <br/><br/>
        <button data-aid="123" @click="eventFn($event)">事件对象</button><br/>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                msg: '你好vue',
                list:[],
            }
        },
        methods:{
            run1(){
                alert("这是第一个方法");
            },
            run2(){
                alert("这是第二个方法");
            },
            getMsg(){
                alert(this.msg);
            },
            setMsg(){
                this.msg = 'Changed'
            },
            requestData(){
                for (var i=0;i<5;i++){
                    this.list.push("我是第" + i + "条信息")
                }
            },
            deleteData(val){
                alert(val);
            },
            eventFn(e){
                console.log(e);
                e.srcElement.style.background = "#7f7f7f";
                console.log(e.srcElement.dataset.aid);/*获取自定义属性值*/
            },
        }
    }
</script>
