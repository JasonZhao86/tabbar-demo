<template>
  <div>
    <MyHeader title="TabBar案例" background="blue" fontColor="white" />
    <div class="main">
      <keep-alive>
        <component :is="comName"></component>
      </keep-alive>
    </div>
    <!-- 底部导航点击切换，子传父技术，将要切换的组件名传出来 -->
    <MyTabBar :arr="tabList" @changeTab="changeTab" />
  </div>
</template>

<script>
import MyHeader from '@/components/MyHeader'
import MyTabBar from '@/components/MyTabBar'
import MyGoodsList from '@/views/MyGoodsList'
import MyGoodsSearch from '@/views/MyGoodsSearch'
import MyUserInfo from '@/views/MyUserInfo'
export default {
  components: {
    MyTabBar,
    MyHeader,
    MyGoodsList,
    MyGoodsSearch,
    MyUserInfo,
  },
  data() {
    return {
      tabList: [
        {
          iconText: 'icon-shangpinliebiao',
          text: '商品列表',
          componentName: 'MyGoodsList',
        },
        {
          iconText: 'icon-sousuo',
          text: '商品搜索',
          componentName: 'MyGoodsSearch',
        },
        {
          iconText: 'icon-user',
          text: '我的信息',
          componentName: 'MyUserInfo',
        },
      ],
      comName: 'MyGoodsList',
    }
  },
  methods: {
    changeTab(componentName) {
      this.comName = componentName
    },
  },
}
</script>

<style scoped>
/* 设置上下内边距 */
.main {
  padding-top: 45px;
  padding-bottom: 51px;
}
</style>
