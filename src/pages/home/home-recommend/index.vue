<template>
<!--  推荐开始 -->
  <view class="recommend_wrap">
    <view
      class = "recommend_item"
      v-for="item in recommends"
      :key="item.id"
      >
      <image mode="widthFix" :src="item.thumb"></image>

    </view>
  </view>
  <!--  推荐结束 -->

</template>

<script>
export default {
  data(){
    return{
      // 推荐列表
      recommends:[]
    }
  },
  mounted() {
    this.request({
      url: "http://157.122.54.189:9088/image/v3/homepage/vertical",
      data:{
        // 要获取几条
        limit:30,
        // 关键字
        order:'hot',
        // 要跳过几条
        skip: 0
      }
    })
    .then(result=>{
      console.log(result);
      this.recommends = result.res.homepage[1].items;
    })
  }
}
</script>

<style lang="scss" scoped>
.recommend_wrap{
  // flex布局
  display: flex;
  flex-wrap: wrap;
  .recommend_item{
    width: 50%;
    border: 5rpx solid #fff;
  }
}

</style>