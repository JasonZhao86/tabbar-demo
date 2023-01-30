<template>
  <div class="my-tab-bar">
    <div
      class="tab-item"
      :class="{ current: activeIndex === index }"
      v-for="(item, index) in arr"
      :key="index"
      @click="changeTab(item, index)"
    >
      <!-- 图标 -->
      <span class="iconfont" :class="item.iconText"></span>
      <!-- 文字 -->
      <span>{{ item.text }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    arr: {
      type: Array,
      required: true,
      validator(list) {
        if (list.length >= 2 && list.length <= 5) {
          return true
        } else {
          console.error('TabBar数据源必须在2-5项')
          return false
        }
      },
    },
  },
  data() {
    return {
      activeIndex: 0,
    }
  },
  methods: {
    changeTab(obj, index) {
      this.activeIndex = index
      this.$emit('changeTab', obj.componentName)
    },
  },
}
</script>

<style lang="less" scoped>
.my-tab-bar {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: white;
  .tab-item {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

.current {
  color: #1d7bff;
}
</style>
