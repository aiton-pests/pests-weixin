# 业主端

## 1 操作界面

### 1.1 扫码操作

### 1.2查看信息

## 2 业务部署

### 2.1 修改项目HTTP地址

请在文件`nuxt.config.js`修改 `baseUrl`

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





## 4 什么是Yarn？




Yarn是Facebook公司出品的用于管理nodejs包的一款软件，开发过nodejs的同学应该知道，我们一般都使用npm作为我们nodejs项目的模块管理器，但npm有一些历史遗留问题:

极其快速。Yarn 会缓存它下载的每个包，所以无需重复下载。它还能并行化操作以最大化资源利用率，安装速度之快前所未有。
特别安全。Yarn会在每个安装包被执行前校验其完整性。
超级可靠。Yarn 使用格式详尽而又简洁的 lockfile文件 和确定性算法来安装依赖，能够保证在一个系统上的运行的安装过程也会以同样的方式运行在其他系统上。


### 安装Yarn


官网下载 https://yarnpkg.com/en/docs/install
(√方便。推荐)快速在NPM 中安装 npm install -g yarn
windows MSI安装,下载地址：https://yarnpkg.com/latest.msi
macOS安装脚本 curl -o- -L https://yarnpkg.com/install.sh | bash
linux安装sudo apt-get update && sudo apt-get install yarn
检查安装

```shell
yarn --version
```


或者

```shell
yarn -v
```



设置阿里云镜像加速

```shell
yarn config set registry "https://registry.npm.taobao.org"
```



### Yarn的基本命令


yarn和yarn install，这两个命令的效果是一样的，等同于npm install，使用这个命令会在该目录生成一个yarn.lock的文件。
yarn add koa，安装koa模块并更新package.json和yarn.lock文件，等同于npm install koa --save。也可以使用yarn global add koa，等同于npm install koa -g，将模块直接安装到全局环境变量里，方便使用。
yarn list，根据当前项目的package.json查看模块的依赖及版本。
yarn info koa，查看koa模块的详细信息，类似于npm view koa。
yarn init，初始化项目package.json文件，等同于npm init。
yarn run，运行package.json中的script。

### NPM与YARN关系对照表




| npm (v5)                              | Yarn                          |
| ------------------------------------- | ----------------------------- |
| npm install                           | yarn install                  |
| (N/A)                                 | yarn add --flat               |
| npm install --no-package-lock         | yarn add --no-lockfile        |
| (N/A)                                 | yarn add --pure-lockfile      |
| npm install [package] --save          | yarn add [package]            |
| npm install [package] --save-dev      | yarn add [package] --dev      |
| (N/A)                                 | yarn add [package] --peer     |
| npm install [package] --save-optional | yarn add [package] --optional |
| npm install [package] --save-exact    | yarn add [package] --exact    |
| (N/A)                                 | yarn add [package] --tilde    |
| npm install [package] --global        | yarn global add [package]     |
| npm update --global                   | yarn global upgrade           |
| npm rebuild                           | yarn add --force              |
| npm uninstall [package]               | yarn remove [package]         |
| rm -rf node_modules && npm install    | yarn upgrade                  |
| npm version major                     | yarn version --major          |
| npm version minor                     | yarn version --minor          |
| npm version patch                     | yarn version --patch          |
| npm cache clean                       | yarn cache clean [package]    |
| (N/A)                                 | yarn add --har                |
