<template>
  <div class="container">
    <h5 id="title" ref="title" class="title">
      {{ title }} - {{ qrcode.codeInt }}
    </h5>
    <el-collapse v-model="activeNames" @change="handleChange">
      <el-collapse-item v-for="item in trapList" :key="item.id" :title="item.village">
        <el-form ref="form" :model="item" label-width="80px">
          <el-form-item label="设备编号">
            <el-input v-model="item.deviceId" />
          </el-form-item>
          <el-form-item label="更换诱芯">
            <el-select v-model="item.lureReplaced" disabled placeholder="请选择">
              <el-option
                v-for="it in options"
                :key="it.value"
                :label="it.text"
                :value="it.value"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="偏移-米">
            <el-input v-model="item.positionError" />
          </el-form-item>
          <el-form-item label="操作员">
            <el-input v-model="item.operator" />
          </el-form-item>
          <el-form-item label="收虫">
            <el-col :span="11">
              <el-input v-model="item.scount" />
            </el-col>
            <el-col class="line" :span="2">
              -
            </el-col>
            <el-col :span="11">
              <el-input v-model="item.remark" />
            </el-col>
          </el-form-item>
          <el-form-item label="时间">
            {{ item.stime | formatDate }}
          </el-form-item>
          <el-form-item label="第一张照片">
            <div class="demo-image">
              <div class="block">
                <el-image
                  style="width: 100%; height: 100%"
                  :src="item.pic1"
                />
              </div>
            </div>
          </el-form-item>
          <el-form-item label="第二张照片">
            <div class="demo-image">
              <div class="block">
                <el-image
                  style="width: 100%; height: 100%"
                  :src="item.pic2"
                />
              </div>
            </div>
          </el-form-item>
          <el-form-item label="经纬度">
            <el-col :span="11">
              <el-input v-model="item.longitude" />
            </el-col>
            <el-col class="line" :span="2">
              -
            </el-col>
            <el-col :span="11">
              <el-input v-model="item.latitude" />
            </el-col>
          </el-form-item>
          <el-form-item label="地址">
            <el-col :span="11">
              <el-input v-model="item.town" />
            </el-col>
            <el-col class="line" :span="2">
              -
            </el-col>
            <el-col :span="11">
              <el-input v-model="item.village" />
            </el-col>
          </el-form-item>
          <el-form-item label="大小班">
            <el-col :span="11">
              <el-input v-model="item.db" />
            </el-col>
            <el-col class="line" :span="2">
              -
            </el-col>
            <el-col :span="11">
              <el-input v-model="item.xb" />
            </el-col>
          </el-form-item>
        </el-form>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {
  filters: {
    formatDate (value) {
      const date = new Date(value)
      const y = date.getFullYear()
      let MM = date.getMonth() + 1
      MM = MM < 10 ? ('0' + MM) : MM
      let d = date.getDate()
      d = d < 10 ? ('0' + d) : d
      let h = date.getHours()
      h = h < 10 ? ('0' + h) : h
      let m = date.getMinutes()
      m = m < 10 ? ('0' + m) : m
      let s = date.getSeconds()
      s = s < 10 ? ('0' + s) : s
      return y + '-' + MM + '-' + d + ' ' + h + ':' + m + ':' + s
    }
  },
  data () {
    return {
      activeNames: ['1'],
      trapList: {},
      member: {},
      project: {},
      qrcode: {},
      showDetail: true,
      title: '绿树防治',
      options: [
        { value: 1, text: '有更换诱芯' },
        { value: 0, text: '没有更换诱芯' }
      ],
      pestsTypeoptions: [
        { value: '诱木', text: '诱木' },
        { value: '诱捕器', text: '诱捕器' },
        { value: '砍倒的树', text: '砍倒的树' }
      ]
    }
  },
  computed: {
    lrelace (val) {
      return val
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
      // eslint-disable-next-line no-console
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
      const pest = await this.$axios.$get(process.env.baseUrl + `/educenter/trap/getByQrcode/${qrcodeStr}`)
      if (pest.success) {
        if (pest.data.trap == null) {
          this.showDetail = false
          this.title = '【二维码】未使用过'
        } else {
          this.trapList = pest.data.trap
        }
      } else {
        this.showDetail = false
        this.title = '无相关数据'
      }
    },
    lrelaces (val) {
      return true
    }
  }
}
</script>

<style>

  .title {
    font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
      "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    display: block;
    font-weight: 300;
    font-size: 40px;
    color: #35495e;
    letter-spacing: 1px;
    text-align: center;
  }
</style>
