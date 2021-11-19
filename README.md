# 业主端

## 1 操作界面

### 1.1 扫码操作



### 1.2查看信息



## 2 业务部署

### 2.1修改项目HTTP地址

在文件`nuxt.config.js`修改 `baseUrl`

```shell
export default {
  // Global page headers: https://go.nuxtjs.dev/config-head
  head: {
    title: 'pests-weixin',
    htmlAttrs: {
      lang: 'en'
    },
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: '' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
  },

  // Global CSS: https://go.nuxtjs.dev/config-css
  css: [
  ],

  // Plugins to run before rendering page: https://go.nuxtjs.dev/config-plugins
  plugins: [
  ],

  // Auto import components: https://go.nuxtjs.dev/config-components
  components: true,

  // Modules for dev and build (recommended): https://go.nuxtjs.dev/config-modules
  buildModules: [
    // https://go.nuxtjs.dev/eslint
    '@nuxtjs/eslint-module'
  ],

  // Modules: https://go.nuxtjs.dev/config-modules
  modules: [
    // https://go.nuxtjs.dev/axios
    '@nuxtjs/axios'
  ],

  // Axios module configuration: https://go.nuxtjs.dev/config-axios
  axios: {},

  // Build Configuration: https://go.nuxtjs.dev/config-build
  build: {
  },
  env: {
    baseUrl: 'https://8222.qiter.com.cn'
  }
}

```

修改`scripts` 下 `dev 、 build 、 start 、 generate、 pm2`参数

```shell
{
  "name": "pests-weixin",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "cross-env baseUrl=https://8222.qiter.com.cn nuxt",
    "build": "cross-env baseUrl=https://8222.qiter.com.cn nuxt build",
    "start": "cross-env baseUrl=https://8222.qiter.com.cn nuxt start",
    "generate": "cross-env baseUrl=https://8222.qiter.com.cn nuxt generate",
    "pm2": "cross-env baseUrl=https://8222.qiter.com.cn nuxt build && pm2 start npm --name web-name -- run start",
    "lint:js": "eslint --ext \".js,.vue\" --ignore-path .gitignore .",
    "lint": "yarn lint:js"
  },
  "dependencies": {
    "@nuxtjs/axios": "^5.12.5",
    "core-js": "^3.8.3",
    "cross-env": "^7.0.3",
    "nuxt": "^2.14.12"
  },
  "config": {
    "nuxt": {
        "host": "0.0.0.0",
        "port": "3000"
    }
  },
  "devDependencies": {
    "@nuxtjs/eslint-config": "^5.0.0",
    "@nuxtjs/eslint-module": "^3.0.2",
    "babel-eslint": "^10.1.0",
    "eslint": "^7.18.0",
    "eslint-plugin-nuxt": "^2.0.0",
    "eslint-plugin-vue": "^7.5.0"
  }
}

```



### 2.2执行build打包

```shell
 npm run build
```

### 2.3拷贝文件到服务器

![](https://pestscontrol.oss-cn-hangzhou.aliyuncs.com/document/depoly/nuxt-copy-file-to-server.png).

![](https://pestscontrol.oss-cn-hangzhou.aliyuncs.com/document/depoly/xftp-copy-file.png)



### 2.4服务器启动

```shell
#切换到项目目录
cd pests_nuxt_202103081/
# 安装依赖包
npm install -production

#pm2 启动项目
pm2 start npm --name pests-nuxt -- run start 


# 服务器自动重启
$ pm2 startup


$ npm install pm2 -g     # 命令行安装 pm2 
$ pm2 start app.js -i 4  # 后台运行pm2，启动4个app.js 
                         # 也可以把'max' 参数传递给 start
                         # 正确的进程数目依赖于Cpu的核心数目
$ pm2 start app.js --name my-api # 命名进程
$ pm2 list               # 显示所有进程状态
$ pm2 monit              # 监视所有进程
$ pm2 logs               # 显示所有进程日志
$ pm2 stop all           # 停止所有进程
$ pm2 restart all        # 重启所有进程
$ pm2 reload all         # 0 秒停机重载进程 (用于 NETWORKED 进程)
$ pm2 stop 0             # 停止指定的进程
$ pm2 restart 0          # 重启指定的进程
$ pm2 startup            # 产生 init 脚本 保持进程活着
$ pm2 web                # 运行健壮的 computer API endpoint (http://localhost:9615)
$ pm2 delete 0           # 杀死指定的进程
$ pm2 delete all         # 杀死全部进程

```



## 3 Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
