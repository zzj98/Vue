<template>
    <div id="vue_det">
        <div>site : {{site}}</div>
        <div>url : {{obj.url}}</div>
        <div>{{details()}}</div>
        <ul>
            <li v-for="item in list">
                {{item}}
            </li>
        </ul>
        <ul>
            <li v-for="item in list1">
                {{item.cate}}
                <ul>
                    <li v-for="news in item.list">
                        {{news.title}}
                    </li>
                </ul>
            </li>
        </ul>
        <div v-bind:title="title">鼠标放上看一下</div>
        <br/>
        <!--绑定数据-->
        <img v-bind:class="{'size':flag}" src="http://www.jituwang.com/uploads/allimg/150130/258900-15013023113365.jpg">&nbsp;
        <img v-bind:class="{'size':flag}" v-bind:src="url"/>&nbsp;
        <img v-bind:class="{'size':flag}" :src="url"/>
        <!--绑定html-->
        <div v-html="h2"></div>
        <!--绑定数据另一种方式-->
        <div v-text="site"></div>
        <ul>
            <li v-for="(item,key) in list2" :class="{'red':key=='0','blue':key=='1'}">
                {{key}}:{{item}}
            </li>
        </ul>
        <div class="box" :style="{'width':boxWdith+'px'}">aaa</div>
        <br/>
        <!--双向数据绑定必须在表单中使用-->
        <label>
            <input type="text" v-model="site"/>
            <button v-on:click="getMsg">获取表单数据</button>
            <button v-on:click="setMsg">set表单数据</button>
        </label>
        <hr>
        <label>
            <input type="text" ref="userinfo"/>
            <div ref="box">I am a box</div>
            <button v-on:click="getInputValue">获取表单数据</button>
        </label>

    </div>
</template>

<script>
    export default {
        data() {  /*业务逻辑里面定义的数据*/
            return {
                site: "菜鸟教程",
                obj: {
                    url: "www.runoob.com",
                },
                list: [1, 2, 3],
                list1: [
                    {
                        "cate": "aaa",
                        "list": [
                            {'title': 'AAA',},
                            {'title': 'AAA',}]
                    },
                    {
                        "cate": "bbb",
                        "list": [
                            {'title': 'BBB',},
                            {'title': 'BBB',}
                        ]
                    }
                ],
                title: 'I am a title',
                url: 'http://www.jituwang.com/uploads/allimg/150130/258900-15013023113365.jpg',
                h2: '<h2>Hello</h2>',
                flag: 'true',
                list2: ['1111', '2222', '3333'],
                boxWdith: 5 * 100,
            }
        },
        methods: {
            /*放置方法的地方*/
            details() {
                return this.site + " - 学的不仅是技术，更是梦想！";
            },
            getMsg() {
                alert("欢迎" + this.site + "使用");
            },
            setMsg() {
                this.site = "I have been changed";
            },
            getInputValue() {
                console.log(this.$refs.userinfo);
                this.$refs.box.style.background = "#7f7f7f";
                alert(this.$refs.userinfo.value);
            },
        }
    }
</script>

<style lang="scss">
    .size {
        width: 100px;
        height: 100px;
    }

    .red {
        color: red;
    }

    .blue {
        color: blue;
    }

    .box {
        width: 100px;
        height: 100px;
        background: #7f7f7f;
    }

    body {
        background: honeydew;
    }
</style>