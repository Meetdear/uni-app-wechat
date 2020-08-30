<template>
    <view>
      <view class="album_bg">
         <image mode="widthFix" :src="album.cover"> </image>
          <view class="album_info">
               <view class="album_name">{{album.name}}</view>
              <view class="album_btn">关注专辑</view>
          </view>
      </view>    
    </view> 
</template>

<script>
export default {
    data(){
        return{
            params:{
               limit:30,
               order:"new",
               skip:0,
               //1 返回值中 有album对象
            //    0 返回值中 只有wallpaper
               first:1
            },
            id:-1,
            album:[],
            wallpaper:[]
           
        }
    },
     onLoad(options){
    //   console.log(options);
      this.id=options.id;
      this.getList();
     },
     methods:{
         getList(){
             this.request({
              url:`http://157.122.54.189:9088/image/v1/wallpaper/album/${this.id}/wallpaper`
         }).then(result=>{
             console.log(result);
             this.album=result.res.album;
             this.wallpaper=result.res.wallpaper;
         })
         }
        
     }
}

</script>

<style lang="scss" scoped>
     .album_bg{
         position: relative;
         image{

         }
         .album_info{
             position:absolute;
             width:100%;
             left:0;
             bottom: 0;
             display: flex;
             justify-content: space-between;
             height:80rpx;
             align-items: center;
             color:#fff;
             padding:0 15rpx;
             .album_name{
                 font-size: 40rpx;
             }
             .album_btn{
                background-color: $color;
                width:152rpx;
                height:50rpx;
                display: flex;
                justify-content: center;
                align-items: center;
                border-radius: 10rpx;
             }
         }
     }
</style>