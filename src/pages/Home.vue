<template>
  <div class="home">
    <PageHeader></PageHeader>
    <div class="img-wrap">
      <div class="text-wrap">
        <p class="title">1. 定投指数基金有什么好？</p>
        <ul class="desc">
          <li>指数长期是看涨的，而现在处于低位，牛市来了指数是不会缺席的；</li>
          <li>指数是永久的，可以躲避黑天鹅，避免在个股上的极大损失；</li>
          <li>定投是最省心最稳妥的投资办法，可以让你实现稳稳的收益。</li>
        </ul>
        <p class="title">2. 定投增强策略是干什么的？</p>
        <ul class="desc">
          <li>在低估值区间，多投入点资金；</li>
          <li>在正常估值值区间，少投入点资金；</li>
          <li>在高估值区间，分批卖出，从而获取超额收益。</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import PageHeader from '../components/PageHeader'

export default {
  data () {
    return {}
  },
  components: {
    'PageHeader': PageHeader
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/pages/Home.scss"
</style>
