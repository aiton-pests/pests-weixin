<template>
  <div class="container">
    <img
      class="imgStyle"
      :src="picurl"
    >
  </div>
</template>

<script>
export default {

  data () {
    return {
      pests: {},
      picurl: '',
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
    // 表单初始化
    init () {
      // debugger
      // eslint-disable-next-line no-console
      console.log('init ： ' + process.env.baseUrl)
      if (this.$route.query && this.$route.query.id && this.$route.query.type) {
        const id = this.$route.query.id
        const type = this.$route.query.type
        this.fetchDataById(id, type)
      } else {
        // 对象拓展运算符：拷贝对象，而不是赋值对象的引用
        // this.pests = { ...defaultForm }
      }
    },
    // 根据id查询记录
    async fetchDataById (id, type) {
      const pest = await this.$axios.$get(process.env.baseUrl + `/educenter/trap/get/${id}`)
      if (pest.success) {
        if (pest.data.teacher != null) {
          this.pests = pest.data.teacher
          if (type === 'pic1') {
            this.picurl = pest.data.teacher.pic1
          } else if (type === 'pic2') {
            this.picurl = pest.data.teacher.pic2
          }
          // eslint-disable-next-line no-console
          console.log(this.pests)
        }
      } else {
        this.showDetail = false
        this.title = '无相关数据'
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.imgStyle{
  width: 100%;
  height: 100%;
}

</style>
