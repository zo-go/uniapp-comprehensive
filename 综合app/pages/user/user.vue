<template>
  <view>
    <image
      src="/static/icons/wallhaven-k7eko6.jpg"
      mode=""
      style="position: fixed; width: 100%; height: 100%; filter: blur(3px); z-index: -1;"
    ></image>
 
    <view
      style="padding: 150rpx 100rpx; display: flex; align-items: center; flex-direction: column;"
    >
      <image
        src="/static/icons/a.png"
        mode=""
        style="background-color: white; width: 400rpx; height: 100rpx; border-radius: 10rpx;"
      ></image>
 
      <view class="input-area">
        <image src="/static/icons/username.png" mode=""></image>
        <input type="text" placeholder="用户名/手机号" />
      </view>
 
      <view class="input-area" style="margin-top: 30rpx;">
        <image src="/static/icons/password.png" mode=""></image>
        <input :type="passwordVisible ? 'text' : 'password'" placeholder="密码" />
        <image
          @click="passwordVisible = !passwordVisible"
          :src="eyeImg"
          style="margin-left: auto;"
          mode=""
        ></image>
      </view>
 
      <view
        hover-class="btn-active"
        style="background-color: orange; width: 100%; margin-top: 40rpx; display: flex; justify-content: center; padding: 15rpx; border-radius: 10rpx;"
      >
        <text style="color: white;">登    录</text>
      </view>
 
      <!-- <view style="margin-top: 30rpx; justify-content: space-between; display: flex; width: 100%; font-size: 0.8em;">
        <view hover-class="btn-active" 
		style="color: rgba(255,255,255,0.5); text-decoration: underline;">
          忘记密码?
        </view>
        <view hover-class="btn-active" 
		style="color: rgba(255,255,255,0.5); text-decoration: underline;">
          立即注册
        </view>
      </view> -->
	  
	  <view style="display: flex;justify-content: space-between; width: 100%;">
		  <view hover-class="btn-active"
		  style="">忘记密码?</view>
		  
		  <view hover-class="btn-active">立即注册</view>
	  </view>
 
      <view style="position: absolute; bottom: 0;">
        <view style="display: flex; width: 100%; align-items: center;">
          <view style="background-color: white; height: 1px; width: 200rpx;"/>
          <text style="color: white; font-size: 0.8em; margin: 0 10rpx;">第三方直接登录</text>
        <view style="background-color: white; height: 1px; width: 200rpx;"/>
        </view>
        <view style="display: flex; width: 100%; justify-content: center; align-items: center;">
          <view hover-class="btn-active">
            <image
              style="width: 90rpx; height: 90rpx;"
              src="/static/icons/qq.png"
              mode=""
            ></image>
          </view>
 
          <view hover-class="btn-active" style="margin: 30rpx 60rpx">
            <image
              style="width: 90rpx; height: 90rpx;"
              src="/static/icons/wx.png"
              mode=""
            ></image>
          </view>
          <view hover-class="btn-active">
            <image
              style="width: 90rpx; height: 90rpx;"
              src="/static/icons/wb.png"
              mode=""
            ></image>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>
 
<script>
export default {
  data() {
    return {
      passwordVisible: false
    };
  },
  methods: {},
  computed: {
    eyeImg() {
      return this.passwordVisible ? '/static/icons/visible.png' : '/static/icons/hidden.png';
    }
  }
};
</script>
 
<style lang="scss">
.input-area {
  background-color: white;
  display: flex;
  padding: 18rpx;
  border-radius: 8rpx;
  margin-top: 100rpx;
  width: 100%;
  align-items: center;
 
  > image {
    width: 40rpx;
    height: 40rpx;
    margin-right: 10rpx;
  }
}
.btn-active {
  opacity: 0.7;
}
</style>