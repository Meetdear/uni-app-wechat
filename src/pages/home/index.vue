<template>
     <view>
         <view class="home_tab">
             <view  class="home_tab_title">
                 <view class="title_inner">
                      <uni-segmented-control :current="current" :values="items.map(v=>v.title)" @clickItem="onClickItem" style-type="text" active-color="#d4237a"></uni-segmented-control>  
                 </view>
                 <view class="iconfont iconsearch"></view>
            </view>
         <view class="content">
            <view v-if="current === 0">
               <home-recommend></home-recommend>
            </view>
            <view v-if="current === 1">
               <home-category></home-category>
            </view>
            <view v-if="current === 2">
                <home-new></home-new>
            </view>
            <view v-if="current === 3">
                <home-album></home-album>
            </view>
          </view>
       </view>
          <!-- 首页
         <text class="iconfont iconvideocamera"></text>  
         <uni-badge text="1"></uni-badge> 
         <uni-badge text="2" type="success" @click="bindClick"></uni-badge>
         <uni-badge text="3" type="primary" :inverted="true"></uni-badge> -->
    </view>
</template>
<script>
// import {uniBadge} from '@dcloudio/uni-ui';
import homeAlbum from './home-album';
import homeCategory from './home-category';
import homeNew from './home-new';
import homeRecommend from './home-recommend';
import {uniSegmentedControl} from '@dcloudio/uni-ui'
export default {
  components:{
    //   uniBadge
    homeAlbum,
    homeCategory,
    homeNew,
    homeRecommend,
    uniSegmentedControl
  }  ,
    data() {
        return {
            items: [
                {title:"推荐"},
                {title:"分类"},
                {title:"最新"},
                {title:"专辑"}
            ],
            current:0
        }
    },
      methods: {
        onClickItem(e) {
            if (this.current !== e.currentIndex) {
                this.current = e.currentIndex;
            }
        }
    },
    // onLoad(){
    //     this.request({
    //      url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
    //     }).then(res=>{
    //         console.log(res);
    //     })
    // }

//   onLoad(){
//       //http://157.122.54.189:9088/image/v3/homepage/vertical

//       //1 原生的微信小程序的api
//       wx.request({
//           url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
//           success(res){
//               console.log(res);
//           }
//       })

//       //2 uni-api
//       uni.request({
//          url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
//       }).then(res=>{
//           console.log(res);
//       })
//   }

};
</script>
<style lang="scss">
  .home_tab{
      .home_tab_title{
       position: relative;
        .title_inner{
            width:60%;
            margin: 0 auto;
        }
        .iconsearch{
            position: absolute;
            top:50%;
            transform:translateY(-50%);
            right:5%;
        }
      }
      .home_tab_content{

      }
  }
</style>