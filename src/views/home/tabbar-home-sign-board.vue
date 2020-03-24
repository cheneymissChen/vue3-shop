<template>


	<div class="signboard">
 <!-- 搜索 -->
  <van-search
  v-model="value"
  shape="round"
  background="#4fc08d"
  placeholder="请输入搜索关键词"
/>

<!-- 轮播图的位置开始 -->
<div class="swipe_container">
<van-swipe :autoplay="3000">
  <van-swipe-item v-for="(image, index) in images" :key="index">
   
    		<img  v-lazy="image"  class="product_img" />
  </van-swipe-item>
</van-swipe>
</div>




		<!-- <img :src="boardUrl" :height="signboardHeight" width="100%"> -->

    <!-- 轮播图位置的结束 -->
		<div class="store_opacity clearfix">
			<div class="float-l">{{storeName}}</div>
			<div class="float-r store_collect isCollect" @click="showCollect = true">
				<van-icon name="shoucang-full" />
				<span>收藏</span>
			</div>
		</div>

		<van-popup v-model="showCollect" position="top" style="background-color: transparent">
			<img :src="showCollect && collectImg" @click="showCollect = false" width="100%" alt="右上角收藏">
		</van-popup>
	</div>
</template>

<script>
import { Popup } from 'vant';
import collectImg from '@/assets/images/index_collect.png';
import Vue from 'vue';
import { Lazyload } from 'vant';

Vue.use(Lazyload);

export default {
  name: 'sign-board',
  props: {
    boardUrl: {
      type: String,
      required: true
    },
    storeName: {
      type: String,
      required: true
    }
  },
  data() {
    const clientW =
      document.body.clientWidth || document.documentElement.clientWidth;
    const signboardHeight = clientW ? (clientW * 2) / 3 : 250;
    return {
      signboardHeight,
      showCollect: false,
      collectImg,
         value: '',
        images: [
       'https://img.yzcdn.cn/vant/cat.jpeg',
       'https://img.yzcdn.cn/vant/apple-1.jpg',
       'https://img.yzcdn.cn/vant/apple-2.jpg'
      ]
    };
  },

  components: {
    [Popup.name]: Popup
  }
};
</script>

<style lang="scss" scoped>

.swipe_container{
        width: 100%;
        height: 200px;
        .van-swipe{
          height:100%;
        }
        .product_img{
          width: 100%;
          height: 100%;
        } 
}
.signboard {
  position: relative;
  min-height: 250px;
}
.store_opacity {
  position: absolute;
  bottom: 0;
  color: #fff;
  width: 100%;
  background-image: linear-gradient(rgba(0, 0, 0, 0), rgba(0, 0, 0, 1));
  padding: 15px 10px;
  box-sizing: border-box;
}

.isCollect i {
  color: $red;
}
</style>
