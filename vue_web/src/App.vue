<template>
  <div id="app-container">
    <!--1.顶部导航条-->
    <mt-header fixed :title="$route.meta.title">
      <a v-show="flag" slot="left" @click="goBack">
        <mt-button icon="back">返回</mt-button>
      </a>
    </mt-header>
    <!--2.中间路由-->
    <transition :name="transitionName">
      <router-view></router-view>
    </transition>
    <!--3.底部tabbar-->
    <nav class="mui-bar mui-bar-tab">
      <router-link class="mui-tab-itemllb" to="/home">
        <span class="mui-icon mui-icon-home"></span>
        <span class="mui-tab-label">首页</span>
      </router-link>
      <router-link class="mui-tab-itemllb" to="/member">
        <span class="mui-icon mui-icon-contact"></span>
        <span class="mui-tab-label">会员</span>
      </router-link>
      <router-link class="mui-tab-itemllb" to="/shopcar">
        <span class="mui-icon mui-icon-extra mui-icon-extra-cart">
            <span id="badge" class="mui-badge">{{ $store.getters.getAllCount }}</span>
        </span>
        <span class="mui-tab-label">购物车</span>
      </router-link>
      <router-link class="mui-tab-itemllb" to="/search">
        <span class="mui-icon mui-icon-search"></span>
        <span class="mui-tab-label">搜索</span>
      </router-link>
    </nav>
  </div>
</template>

<script>
  export default {
    data:function(){
      return {
        //flag只是用来表示返回按钮是否需要显示
        flag:this.$route.path !== '/home',
        //isBack用来标识当前的操作是前进还是后退
        isBack:false ,
        transitionName: 'slide-right'
      }
    },
    methods:{
      goBack(){
        this.isBack = true;
        this.$router.go(-1);
      }
    },
    watch:{
      '$route.path':function(newVal,oldVal){
        if(this.isBack){
          this.transitionName = 'slide-right'
        }
        else{
          this.transitionName = 'slide-left'
        }
        this.isBack = false;

        if(newVal != '/home'){
          this.flag = true;
        }
        else{
          this.flag = false;
        }
      }
    }
  }
</script>

<style lang="less">
  #app-container{
    padding-top: 40px;
    padding-bottom: 40px;
    /*避免PC端网页在页面切换的时候出现的水平滚动条*/
    overflow: hidden;
    overflow-x: hidden;
    overflow-y: hidden;
  }
  body{
    touch-action: none;
  }
  .mui-bar-tab .mui-tab-itemllb
  {
    display: table-cell;
    overflow: hidden;

    width: 1%;
    height: 50px;

    text-align: center;
    vertical-align: middle;
    white-space: nowrap;
    text-overflow: ellipsis;

    color: #929292;
  }
  .mui-bar-tab .mui-tab-itemllb.mui-active
  {
    color: #007aff;
  }
  .mui-bar-tab .mui-tab-itemllb .mui-icon
  {
    top: 3px;

    width: 24px;
    height: 24px;
    padding-top: 0;
    padding-bottom: 0;
  }
  .mui-bar-tab .mui-tab-itemllb .mui-icon ~ .mui-tab-label
  {
    font-size: 11px;

    display: block;
    overflow: hidden;

    text-overflow: ellipsis;
  }
  .mui-bar-tab .mui-tab-itemllb .mui-icon:active
  {
    background: none;
  }


  /*左边进入*/
  .slide-left-enter{
    -webkit-transform: translate(100%, 0);
    transform: translate(100%, 0);
  }
  /*左边离开*/
  .slide-left-leave-to{
    -webkit-transform: translate(-100%, 0);
    transform: translate(-100% 0);
    position: absolute;
  }

  /*右边进入*/
  .slide-right-enter {
    -webkit-transform: translate(-100%, 0);
    transform: translate(-100% 0);
  }
  /*右边离开*/
  .slide-right-leave-to {
    -webkit-transform: translate(100%, 0);
    transform: translate(100%, 0);
    position: absolute;
  }

  /*进入退出动画*/
  .slide-right-enter-active,
  .slide-left-enter-active,
  .slide-right-leave-active,
  .slide-left-leave-active {
    transition: all 0.5s ease;
  }

  /*左边进入*/
  .slide-left-enter{
    -webkit-transform: translate(100%, 0);
    transform: translate(100%, 0);
  }
  /*左边离开*/
  .slide-left-leave-to{
    -webkit-transform: translate(-100%, 0);
    transform: translate(-100% 0);
    position: absolute;
  }

  /*右边进入*/
  .slide-right-enter {
    -webkit-transform: translate(-100%, 0);
    transform: translate(-100% 0);
  }
  /*右边离开*/
  .slide-right-leave-to {
    -webkit-transform: translate(100%, 0);
    transform: translate(100%, 0);
    position: absolute;
  }

  /*进入退出动画*/
  .slide-right-enter-active,
  .slide-left-enter-active,
  .slide-right-leave-active,
  .slide-left-leave-active {
    transition: all 0.5s ease;
  }

</style>
