<template>
    <view @click="handleClick">
        <slot></slot>
    </view>
</template>

<script> 
    export default { 
        props:{
            // 数组
            list:Array,
            // 索引
            index:Number
        },
        // mounted(){
         
        //     // console.log(this.list);
        //     // console.log(this.index);
        // },
        methods:{
           handleClick(){
          //1将数据缓存下来
          getApp().globalData.imgList=this.list;
          getApp().globalData.imgIndex=this.index;
          //2在实现点击跳转
              uni.navigateTo({
                  url:"/pages/imgDetail/index"
              })
            }
        },
    }
</script>

<style scoped>

</style>