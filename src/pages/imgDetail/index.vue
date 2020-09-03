<template>
   <view>
       <!-- 用户信息 开始 -->
      <view class="user_info">
          <view class="user_icon"><image mode="widthFix" :src="imgDetail.user.avatar"></image>
          </view>
         <view class="user_desc">
          <view class="user_name">{{imgDetail.user.name}}</view>
          <view class="user_time">{{imgDetail.cnTime}}</view>
         </view>
      </view>
       <!-- 用户信息 结束-->

       <!-- 高清大图 开始 -->
        <view class="high_img">
           <image mode="widthFix" :src="imgDetail.newThumb"></image>
        </view>
       <!-- 高清大图 结束 -->

       <!-- 点赞 开始 -->
         <view class="user_rank">
            <view class="rank">
               <text class="iconfont icondianzan">{{imgDetail.rank}}</text>
            </view>
            <view class="user_collect">
               <text class="iconfont iconshoucang">收藏</text>
            </view>
         </view>
       <!-- 点赞 结束 -->

       <!-- 专辑 开始 -->
        <view class="album_wrap" v-if="album.length">
           <!-- 标题 -->
           <view class="album_title">相关</view>
           <!-- 内容 -->
           <view class="album_list">
              <view class="album_item"
              v-for="item in album" 
              :key="item.id">


                 <view class="album_cover">
                    <image :src="item.cover" mode="aspectFill"> </image>
                 </view>
                 <!-- 右边 -->
                 <view class="album_info">
                    <view class="album_info_text">专辑</view>
                    <view class="album_name">{{item.name}}</view>
                     <text class=" iconfont iconiconfontjiantou4"></text>
                 </view>
              </view>
           </view>
        </view>
       <!-- 专辑 结束 -->

       <!-- 最新评论 comment hot  -->
        <view class="comment hot">
          <view class="comment_title">
            <text class="iconfont iconhot1"></text>
            <text class="comment_text">最新评论</text>
          </view>
          
          <view class="comment_list">
            <view class="comment_item"
            v-for="item in hot"
            :key="item.id">
            <!-- 用户信息 -->
             <view class="comment_user">
               <!-- 用户头像 -->
               <view class="user-icon">
                  <image :src="item.user.avatar"></image>
               </view>
               <!-- 用户名称 -->
            <view class="user_name">
               <view class="user_nickname">{{item.user.name}}</view>
               <view class="user_time">{{item.atime}}</view>
            </view>
            <!-- 评论数据 -->
            <view class="comment_desc">
               <image></image>
            </view>
          </view>
       </view>
      </view>
   </view>
</template>
    
<script>  

 import moment from "moment";
//  设置语言为中文
moment.locale("zh-cn");
   export default{  
      data(){  
         return{
            // 图片信息对象 包含着用户头像
            imgDetail:{},
            // 专辑数据 数组
            album:[],
            // 最热评论
            hot:[],
            //  最新评论
            comment:[],
            // 图片索引
            imgIndex:0
         }
      },
    onLoad(){
        console.log(getApp().globalData);
        const {imgList,imgIndex}=getApp().globalData;
        this.imgDetail=imgList[imgIndex];
      //   下面是防止报错信息 又能显示出来的做法=>高清图片
        this.imgDetail.newThumb=this.imgDetail.thumb+this.imgDetail.rule.replace('$<Height>',360);
      
      //   xxx年前的数据
      this.imgDetail.cnTime=moment(this.imgDetail.atime*1000).fromNow();

      // 获取图片详情的id
     // this.imgDetail.id
      this.getComments(this.imgDetail.id);
    },
    methods:{
       getComments(id){
          this.request({
                url:`http://157.122.54.189:9088/image/v2/wallpaper/wallpaper/${id}/comment`
                
          }).then(result=>{
            // console.log(result);
             this.album=result.res.album;
             this.hot=result.res.hot;
             this.comment=result.res.comment;
             
          })
       }
    }
   }
</script>
  
 <style lang="scss">
     .user_info {
        display:flex;
       padding:20rpx;
     .user_icon {
        padding: 0 20rpx;
    image{
      width:88rpx;
      border-radius:50%;
    }
  }

  .user_desc {
    .user_name {
       color:#000;
       font-weight: 600;
    }

    .user_time {
       color:#ccc;
       font-size:24rpx;
       padding: 10rpx 0;
    }
  }
}
 
.user_rank {
   display: flex;
   height: 80rpx;
   border-bottom: 5rpx solid #eee;
  
  .rank {
     display: flex;
     justify-content: center;
     align-items: center;
     flex:1;
    .iconfont {
      
    }
  } 
   .user_collect{
      flex:1;
      display: flex;
      justify-content: center;
      align-items: center;
    .iconfont {
      }  
    }
}

// 专辑
.album_wrap {
   padding:20rpx;

  .album_title {
   padding:10rpx 0;
  }

  .album_list {
    .album_item {
       display: flex;
       padding: 10rpx 0;
       border-bottom: 10rpx solid #eee;
      .album_cover {
         flex:1;
        image {
         width:188rpx;
         height:180rpx;
        }
      }

    

      .album_info {
      flex:3;
      padding-left: 20rpx;
      position: relative;
        .album_info_text {
       width:100rpx;
       height:50rpx;
       background-color: $color;
       color:#fff;
       display: flex;
       justify-content: center;
       align-items:center;
        }

        .album_name {
         padding:10rpx 0;
         color:#888;
        }
        .iconfont{
           font-size:40rpx;
           position: absolute;
           top:50%;
            //   css3 变换
           transform:translateY(-50%);
           right:10%;
           color:#000;
       
        }
      }
    }
  }
}

// 最热评论
.comment.hot {
  .comment_title {
        padding:15rpx;
    .iconfont{
      color:red;
      font-size:40rpx; 
      
    }

   .comment_text {
      font-weight: 600;
      font-size:28rpx;
      color:#666;
      margin-left:10rpx;
    }
  }

  .comment_list {

  }
}
 </style>