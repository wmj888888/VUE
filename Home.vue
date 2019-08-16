<template>
    <div>
        <!-- 父面板 -->
        <mt-tab-container v-model="active">
            <!-- 子面板 -->
            <mt-tab-container-item id="index">
                <index></index>  <!--首页-->
            </mt-tab-container-item>    
            <mt-tab-container-item id="cart">
                <cart></cart>    <!--购物车-->
            </mt-tab-container-item> 
            <mt-tab-container-item id="me">
                <my></my>        <!--我的-->
            </mt-tab-container-item> 
        </mt-tab-container>

            <!-- 底部导航条父元素 -->
            <mt-tabbar v-model="active" fixed>
                <!-- 按钮 -->
                <mt-tab-item id="index" @click.native="changeState(0)">
                   <tabbarlcon 
                   :Cp1Image="require('../assets/cp2.png')"
                   :Cp2Image="require('../assets/cp1.png')"
                   :focused="currentIndex[0].isSelect"
                   >
                   </tabbarlcon>
                    首页
                </mt-tab-item>
            
                <mt-tab-item id="cart" @click.native="changeState(1)">
                    <tabbarlcon 
                   :Cp1Image="require('../assets/cp4.png')"
                   :Cp2Image="require('../assets/cp3.png')"
                   :focused="currentIndex[1].isSelect"
                   >
                   </tabbarlcon>
                    购物车
                </mt-tab-item>
            
                <mt-tab-item id="me" @click.native="changeState(2)">
                    <tabbarlcon 
                   :Cp1Image="require('../assets/cp6.png')"
                   :Cp2Image="require('../assets/cp5.png')"
                   :focused="currentIndex[2].isSelect"
                   >
                   </tabbarlcon>
                    我的
                </mt-tab-item>
            </mt-tabbar>
    </div>
</template>
<script>
//1.引入子组件
import Index from "./common/Index"  //首页
import Cart from "./cart/Cart"      //购物车
import My from "./common/My"        //我的
import TabBarlcon from "./common/TabBarlcon"

export default {
    data(){
        return{
             active:"index",//保存显示子面板的id
             //在data添加属性    currentIndex
            //集中保存所有按钮状态
            currentIndex:[
                {isSelect:true},  //下标0  保存第一个按钮状态
                {isSelect:false}, //下标1  保存第二个按钮状态
                {isSelect:false}, //下标2  保存第三个按钮状态
            ]
        }
    },
    methods: {
       changeState(idx){
           //指定当前的按钮状态修改为true
           //  其他的按钮状态为     false
            //1.创建循环遍历状态数组
            for(var i=0;i<this.currentIndex.length;i++){
            //2.获取用户点击下标与当前数据元素下标比较
            //3.如果两个值相等当前状态true
                if(idx==i){
                    this.currentIndex[i].isSelect=true;
                }else{
                     //4.其他元素状态false
                     this.currentIndex[i].isSelect=false;
                }
           
            }
       },
    },
    props:{
        //数据msg默认值""

    },
components:{//2.注册子组件
    "index":Index, //首页
    "cart":Cart,   //购物车
    "my":My,       //我的
    "tabbarlcon":TabBarlcon, //底部导航栏
  }
}
</script>
<style  scoped>
    /* 修改组件默认的样式  按钮默认样式*/
    .mint-tab-item-label {
    color: #1f1f1f;
    font-size: 14px !important;
    }
    /* 按钮选中样式 */
    .mint-tabbar > .mint-tab-item.is-selected{
        color:#444 ;
        background-color: #ffffff;
    }

    .mint-tabbar{
        background: #ffffff
    }

</style>