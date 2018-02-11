# vue-component-dataTransfer

1.还在vue项目中慢慢爬坑，在vue项目中传递数据，其中有父组件向子组件，子组件向父组件，以及子组件之间的传递。

2.其中子组件向父组件传递数据，即在子组件vue文件中定义触发方法，将值通过$emit的方式写function

a.子组件navbar.vue

点击tabbar_item时，触发clickFun方法，此处是要传递index

        <div class="weui-tabbar__item"
           v-for="(tabbarName,index) in tabbarNames" v-on:click="clickFun(tabbarName,index) ">
        </div>


方法内容：

使用使用了 $emit 来遍历 transferNav 事件，并返回index

        methods:{
             clickFun(tabbarName,index){
                 this.$emit('transferNav',index);
                 console.log(index);
             },
         }


b.父组件index.vue

    <!--底部导航栏-->

        <navbar @transferNav="getNav"></navbar>

通过方法获取到子组件的传值

         getNav(msg){
             this.userNav = msg;
         },

父组件存放该数据的位置

        <div>{{userNav}}</div>

3 . 父组件向子组件传递

在 Vue 中，可以使用 props 向子组件传递数据。

a.父组件 index.vue

<selfcenter :Indexmsg="Indexmsg"></selfcenter>

在data中定义Indexmsg这个数据变量

        data(){
            return{
                Indexmsg:'data',
            }
        },

b.子组件 selfcenter.vue

子组件中准备好容器存放传递过来的数据

        <div>{{Indexmsg}}</div>

Indexmsg 是在 data 中定义的变量。

如果需要从父组件获取 logo 的值，就需要使用

        props:['Indexmsg']

此时在props中定义后，就不用在data中声明了

4.子组件同级之间的传递，暂时没有有效的方法，可以学习使用vuex，完美解决子组件传递问题

建议组件之间含有数据传递的写在同一个组件内