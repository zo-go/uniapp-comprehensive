<template>
  <view>
    
     
    <uni-load-more :status="status"></uni-load-more>
  </view>
</template>
 
<script>
  export default {
    data() {
      return {
        status:'more',
      }
    },
    mounted() {
    },
    onPullDownRefresh() {
      uni.request({
        url: this.url,
        method: 'GET',
        data: {},
        success: res => {
          console.log(res);
           
          this.data = res.data;
           
          uni.stopPullDownRefresh();
        },
        fail: () => {},
        complete: () => {}
      });
    },
   
    methods: {
     
    }
  }
</script>
 
<style>
.title{
  line-clamp: 2;
  overflow: hidden;
  text-overflow: ellipsis;
  -webkit-box-orient:vertical;
  -webkit-line-clamp:2;
  display: -webkit-box;
}
</style>