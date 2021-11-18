<template>
  <div class="container">
    <el-collapse v-model="activeNames" @change="handleChange">
      <el-collapse-item title="一致性 Consistency" name="1">
        <div>与现实生活一致：与现实生活的流程、逻辑保持一致，遵循用户习惯的语言和概念；</div>
        <div>在界面中一致：所有的元素和结构需保持一致，比如：设计样式、图标和文本、元素的位置等。</div>
      </el-collapse-item>
      <el-collapse-item title="反馈 Feedback" name="2">
        <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
        <div>页面反馈：操作后，通过页面元素的变化清晰地展现当前状态。</div>
      </el-collapse-item>
      <el-collapse-item title="效率 Efficiency" name="3">
        <div>简化流程：设计简洁直观的操作流程；</div>
        <div>清晰明确：语言表达清晰且表意明确，让用户快速理解进而作出决策；</div>
        <div>帮助用户识别：界面简单直白，让用户快速识别而非回忆，减少用户记忆负担。</div>
      </el-collapse-item>
      <el-collapse-item title="可控 Controllability" name="4">
        <div>用户决策：根据场景可给予用户操作建议或安全提示，但不能代替用户进行决策；</div>
        <div>结果可控：用户可以自由的进行操作，包括撤销、回退和终止当前操作等。</div>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {

  data () {
    return {
      activeNames: ['1'],
      pests: {},
      member: {},
      project: {},
      qrcode: {},
      showDetail: true,
      title: '绿树防治',
      options: [
        { value: 1, text: '已删除' },
        { value: 0, text: '未删除' }
      ],
      pestsTypeoptions: [
        { value: '诱木', text: '诱木' },
        { value: '诱捕器', text: '诱捕器' },
        { value: '砍倒的树', text: '砍倒的树' }
      ]
    }
  },
  // 监听器
  watch: {
    $route (to, from) {
      // console.log('路由变化......')
      // console.log(to)
      // console.log(from)
      this.init()
    }
  },

  // 生命周期方法（在路由切换，组件不变的情况下不会被调用）
  created () {
    // console.log('form created ......')
    this.init()
  },

  methods: {
    handleChange (val) {
      console.log(val)
    },
    // 表单初始化
    init () {
      // debugger
      // eslint-disable-next-line no-console
      console.log('init ： ' + process.env.baseUrl)
      if (this.$route.query && this.$route.query.qrcode) {
        const qrcodeStr = this.$route.query.qrcode
        this.fetchDataById(qrcodeStr)
        this.fetchQrcodeByQrcode(qrcodeStr)
      } else {
        // 对象拓展运算符：拷贝对象，而不是赋值对象的引用
        // this.pests = { ...defaultForm }
      }
    },
    async fetchQrcodeByQrcode (qrcodeStr) {
      const qrcodeObje = await this.$axios.$get(process.env.baseUrl + `/educenter/qrcode/getOneByQrcode/${qrcodeStr}`)
      if (qrcodeObje.success) {
        if (qrcodeObje.data.teacher == null) {
          // eslint-disable-next-line no-console
          console.log('')
          // this.showDetail = false
          // this.title = '无【二维码数据】和【' + this.title + '】'
        } else {
          this.qrcode = qrcodeObje.data.teacher
          // eslint-disable-next-line no-console
          console.log(this.qrcode)
        }
      } else {
        this.showDetail = false
        this.title = '无相关数据'
      }
    },
    // 根据id查询记录
    async fetchDataById (qrcodeStr) {
      const pest = await this.$axios.$get(process.env.baseUrl + `/educenter/pests/getPestsControlByQrcode/${qrcodeStr}`)
      if (pest.success) {
        if (pest.data.teacher == null) {
          // eslint-disable-next-line no-console
          console.log('')
          this.showDetail = false
          this.title = '【二维码】未使用过'
        } else {
          this.pests = pest.data.teacher
          // eslint-disable-next-line no-console
          console.log(this.pests)
        }
      } else {
        this.showDetail = false
        this.title = '无相关数据'
      }

      // pestsApi.getByQrcode(qrcode).then((response) => {
      //   this.pests = response.data.teacher
      //   projectApi.getById(this.pests.userId).then((response) => {
      //     this.project = response.data.teacher
      //   })
      //   memberApi.getById(this.pests.projectId).then((response) => {
      //     this.member = response.data.teacher
      //   })
      //   qrcodeApi.getOneByQrcode(this.pests.qrcode).then((response) => {
      //     this.qrcode = response.data.teacher
      //   })
      // })
    }
  }
}
</script>

<style>

</style>
