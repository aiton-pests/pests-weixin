<template>
  <div class="container">
    <div>
      <Logo />
      <h5 id="title" ref="title" class="title">
        {{ title }}
      </h5>
      <div v-show="showDetail" id="detail" ref="detail" class="links">
        <div id="selected_rcds_detail" style="">
          <table id="select_detail_basic_tbl" class="field_value_tbl">
            <tbody>
              <tr>
                <td class="name_column">
                  采集时间
                </td>
                <td class="value_column">
                  {{ pests.stime | formatDate }}
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  采集设备
                </td>
                <td class="value_column">
                  {{ pests.deviceId }}
                </td>
              </tr>
            </tbody>
          </table>
          <table
            id="selected_rcd_detail_pp_tbl"
            class="field_value_tbl"
            data-recordid="14638"
          >
            <tbody>
              <tr>
                <td class="name_column">
                  业务类型
                </td>
                <td class="value_column">
                  {{ pests.pestsType }}
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  树径
                </td>
                <td class="value_column">
                  {{ pests.treeWalk }}
                </td>
              </tr>
              <tr>
                <td colspan="2" class="photo_column">
                  <div
                    class="photo_box loaded"
                    data-ossfile="mpld_3_73_rcd_14638_606.jpg"
                    style="height: 380px;"
                  >
                    <img
                      class="imgStyle"
                      :src="pests.fellPic"
                    >
                    <div class="photo_name">
                      砍倒照片
                    </div>
                    <div class="photo_failed_msg" style="display: none;">
                      无法加载此图片！
                    </div>
                    <div class="photo_busy_ind" style="display: none;" />
                  </div>
                </td>
              </tr>
              <tr>
                <td colspan="2" class="photo_column">
                  <div
                    class="photo_box loaded"
                    data-ossfile="mpld_3_73_rcd_14638_606.jpg"
                    style="height: 380px;"
                  >
                    <img
                      class="imgStyle"
                      :src="pests.stumpPic"
                    >
                    <div class="photo_name">
                      树桩照片
                    </div>
                    <div class="photo_failed_msg" style="display: none;">
                      无法加载此图片！
                    </div>
                    <div class="photo_busy_ind" style="display: none;" />
                  </div>
                </td>
              </tr>
              <tr>
                <td colspan="2" class="photo_column">
                  <div
                    class="photo_box loaded"
                    data-ossfile="mpld_3_73_rcd_14638_607.jpg"
                    style="height: 380px;"
                  >
                    <img
                      class="imgStyle"
                      :src="pests.finishPic"
                    >
                    <div class="photo_name">
                      处理好照片
                    </div>
                    <div class="photo_failed_msg" style="display: none;">
                      无法加载此图片！
                    </div>
                    <div class="photo_busy_ind" style="display: none;" />
                  </div>
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  镇
                </td>
                <td class="value_column">
                  {{ pests.town }}
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  村
                </td>
                <td class="value_column">
                  {{ pests.village }}
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  作业人
                </td>
                <td class="value_column">
                  {{ pests.operator }}
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  小班
                </td>
                <td class="value_column">
                  <div class="action_text record_detail_link" data-recordid="17499">
                    {{ pests.xb }}
                  </div>
                </td>
              </tr>
              <tr>
                <td class="name_column">
                  大班
                </td>
                <td class="value_column">
                  {{ pests.db }}
                </td>
              </tr>
            </tbody>
          </table>
          <table class="field_value_tbl" data-recordid="14638">
            <tbody>
              <tr>
                <td class="name_column">
                  二维码编号
                </td>
                <td class="value_column">
                  <div class="action_text entity_detail_link" data-entityid="17499">
                    {{ pests.qrcode }}
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
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
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.imgStyle{
  width: 400px;
  height: 400px;
}
.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 40px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.name_column {
        min-width: 120px;
        border-right: 1px solid #ececec;
        background-color: #fafafa;
      }
      .value_column {
        width: 50%;
        padding: 0.6em;
        border-bottom: 1px solid #ececec;
      }
      .field_value_tbl {
        border-spacing: 0;
        border-collapse: collapse;
        width: 100%;
        margin: 16px 0 0 0;
      }
      .photo_column {
        padding: 0;
        background-color: #fafafa;
        overflow: hidden;
      }
      .photo_box {
        position: relative;
        min-height: 150px;
      }
      .photo_name {
        position: absolute;
        padding: 4px 16px;
        top: 15px;
        left: 15px;
        border-radius: 3px;
        background-color: rgba(0, 0, 0, 0.38);
        color: white;
      }
      .photo_failed_msg {
        display: none;
        position: relative;
        margin-top: 32px;
        color: #f41616;
      }
      .photo_busy_ind {
        display: none;
        position: absolute;
        left: 50%;
        top: 50%;
        height: 40px;
        width: 40px;
        margin-left: -20px;
        margin-top: -20px;
        -webkit-animation: rotation 0.6s infinite linear;
        -moz-animation: rotation 0.6s infinite linear;
        -o-animation: rotation 0.6s infinite linear;
        animation: rotation 0.6s infinite linear;
        border-left: 4px solid #c3c3c3;
        border-right: 4px solid #c3c3c3;
        border-bottom: 4px solid #c3c3c3;
        border-top: 4px solid #777;
        -webkit-border-radius: 100%;
        -moz-border-radius: 100%;
        -ms-border-radius: 100%;
        -o-border-radius: 100%;
        border-radius: 100%;
      }
      .delete_rcd_button {
        margin: 1em 0;
        padding: 0.8em;
        background-color: red;
        border-radius: 4px;
      }
      .button {
        text-align: center;
        cursor: pointer;
        overflow: visible;
        text-decoration: none;
        color: white;
        background-color: #007aff;
      }
</style>
