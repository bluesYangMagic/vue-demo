<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import header from 'components/header/header.vue';
  import axios from 'axios';

  // 请求返回状态码
  // 0：正常
  const ERR_OK = 0;

  export default {
    // 数据驱动
    // 数据seller
    data() {
      return {
        seller: {}
      };
    },
    // 生命周期
    created() {
      // 数据请求
      axios({
        method: 'get',
        url: '/api/seller'
      }).then(response => {
        // 成功回调
        // console.log(response.data);
        if (response.data.errno === ERR_OK) {
          // 错误状态码为0 数据正常
          // 赋值给 vue实例的seller
          this.seller = response.data.data;
          // console.log(this.seller);
        }
      });
    },
    methods: {
      aaa() {
      }
    },
    mounted() {
      // this.aaa();
    },
    // 注册组件
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus">
  @import "./common/stylus/mixin.styl"

  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        &.active
          color: rgb(240, 20, 20)
</style>
