<template>
  <van-list v-model="infiniteList.isLoading" :finished="infiniteList.isFinished"
            finished-text="没有更多了" @load="infiniteList.onLoadMore"
            :immediate-check="immediateCheck" :offset="offset">
    <slot name="list" />

    <slot name="noData" />
  </van-list>
</template>

<script>

/**
   * 下拉刷新列表组件,包含下拉刷新和无限加载功能，
   * 使用时需传入一个 infiniteList 对象，里面必须包含五个属性，分别表示：
   * 下拉刷新的状态和回调函数，加载更多的状态，是否加载完成和回调函数
   * infiniteList: {
          isLoading: false,
          isFinished: false,
          onLoadMore: () => {
            this.onLoadMore()
          },
        },
   * vant 的 list 组件有个 bug，当它与其他 vant 组件一起使用时，
   * 会导致在页面加载完成时马上触发 onLoadMore 方法，即使设置了 immediate-check 也没有效果
   */
export default {
  name: 'InfiniteList',
  data() {
    return {
      offset: 100,
      immediateCheck: false
    }
  },
  props: {
    infiniteList: {
      type: Object,
      require: true
    }
  }
}
</script>
