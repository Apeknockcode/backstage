# vite-vue3-ts

[![ci](https://github.com/JS-banana/vite-vue3-ts/actions/workflows/deploy.yml/badge.svg)](https://github.com/JS-banana/vite-vue3-ts/actions/workflows/deploy.yml)

## 介绍

一个使用 `vite` + `vue3` + `pinia` + `ant-design-vue` + `typescript` 完整技术路线开发的项目，秒级开发更新启动、新的`vue3 composition api` 结合 `setup`纵享丝滑般的开发体验、全新的 `pinia`状态管理器和优秀的设计体验（`1k`的size）、`antd`无障碍过渡使用UI组件库 `ant-design-vue`、安全高效的 `typescript`类型支持、代码规范验证、多级别的权限管理~


## 特性

- ✨脚手架工具：高效、快速的 **Vite**
- 🔥前端框架：眼下最时髦的 **Vue3**
- 🍍状态管理器：`vue3`新秀 **Pinia**，犹如 `react zustand`般的体验，友好的api和异步处理
- 🏆开发语言：政治正确 **TypeScript**
- 🎉UI组件：`antd`开发者无障碍过渡使用 **ant-design-vue**，熟悉的配方熟悉的味道
- 🎨css样式：**less** 、`postcss`
- 📖代码规范：**Eslint**、**Prettier**、**Commitlint**
- 🔒权限管理：页面级、菜单级、按钮级、接口级
- ✊依赖按需加载：**unplugin-auto-import**，可自动导入使用到的`vue`、`vue-router`等依赖
- 💪组件按需导入：**unplugin-vue-components**，无论是第三方UI组件还是自定义组件都可实现自动按需导入以及`TS`语法提示

## 项目目录

```js
├── .husky                              // husky git hooks配置目录
    ├── _                               // husky 脚本生成的目录文件
    ├── commit-msg                      // commit-msg钩子，用于验证 message格式
    ├── pre-commit                      // pre-commit钩子，主要是和eslint配合
├── config                              // 全局配置文件
    ├── vite                            // vite 相关配置
    ├── constant.ts                     // 项目配置
    ├── themeConfig.ts                  // 主题配置
├── dist                                // 默认的 build 输出目录
├── mock                                // 前端数据mock
├── public                              // vite项目下的静态目录
└── src                                 // 源码目录
    ├── api                             // 接口相关
    ├── assets                          // 公共的文件（如image、css、font等）
    ├── components                      // 项目组件
    ├── directives                      // 自定义 指令
    ├── enums                           // 自定义 常量（枚举写法）
    ├── hooks                           // 自定义 hooks
    ├── layout                          // 全局布局
    ├── router                          // 路由
    ├── store                           // 状态管理器《
    ├── utils                           // 工具库
    ├── views                           // 页面模块目录
        ├── login                       // login页面模块
        ├── ...
    ├── App.vue                         // vue顶层文件
    ├── auto-imports.d.ts               // unplugin-auto-import 插件生成
    ├── components.d.d.ts               // unplugin-vue-components 插件生成
    ├── main.ts                         // 项目入口文件
    ├── shimes-vue.d.ts                 // vite默认ts类型文件
    ├── types                           // 项目type类型定义文件夹
├── .editorconfig                       // IDE格式规范
├── .env                                // 环境变量
├── .eslintignore                       // eslint忽略
├── .eslintrc                           // eslint配置文件
├── .gitignore                          // git忽略
├── .npmrc                              // npm配置文件
├── .prettierignore                     // prettierc忽略
├── .prettierrc                         // prettierc配置文件
├── index.html                          // 入口文件
├── LICENSE.md                          // LICENSE
├── package.json                        // package
├── pnpm-lock.yaml                      // pnpm-lock
├── postcss.config.js                   // postcss
├── README.md                           // README
├── tsconfig.json                       // typescript配置文件
└── vite.config.ts                      // vite
```

## 使用说明

> 简要说明：
>
> 随着vite3.x的发布，本项目针对该依赖的相关生态做了升级，详情见分支 [feat-vite3.x](https://github.com/JS-banana/vite-vue3-ts/tree/feat-vite3.x)
>
> 需要指出的是vite3.x要求node14.18及以上，详情见 [从 v2 迁移](https://cn.vitejs.dev/guide/migration.html)

1. 安装依赖

    ```sh
    # 推荐使用 pnpm
    pnpm install
    # 没有安装的直接安装
    npm install -g pnpm
    ```

2. 启动项目

    ```sh
    pnpm serve
    # or
    pnpm dev
    ```

3. 部署

    ```sh
    # 检查TS类型然后构建打包
    pnpm build:check
    # 跳过检查直接构建打包
    pnpm build
    # 预览
    pnpm preview
    ```

### 数据模拟

为了实现更多元化和真实数据展示，使用了Mock+fakerjs进行数据模拟，fakerjs的功能极其强大，几乎可以定制任何类型数据，本项目里做了部分演示，源码见`mock/table.ts`

### ant-design-vue 2.x升级到3.x的说明

Table组件：

在2.x版本的时候，Table组件主要通过 `columns`属性，配置字段 `slots: { customRender: 'action' }`进行自定义插槽，做到制定内容的内容，基于此，本项目Table组件封装的内部实现为`<template v-if="column.slots?.customRender === 'action'">`。

但是在3.x之后，官方舍弃了 columns中的`slots`属性，因此该方式需要做出调整，不过，我们的整体思路不变，即，确定一个通用且唯一的key为判断属性即可，以实现对不同内容的区别渲染。

目前的方案打算以columns中的`key` prop属性作为唯一判断的key，Table组件封装内部实现如`<template v-if="column.key === 'action'">`，因此，在columns中默认以`dataIndex`作为渲染key，而`key`作为我们的自定义渲染插槽内容的key。

官网API介绍如下：

| Property  | Description                                                                          | Type            | Default |
| --------- | ------------------------------------------------------------------------------------ | --------------- | ------- |
| dataIndex | Display field of the data record, support nest path by string array                  | string/string[] | -       |
| key       | Unique key of this column, you can ignore this prop if you've set a unique dataIndex | string          | -       |

### Table高级组件的基本用法

> 详情及源码见：./src/components/Table/index.vue

几个核心API：

| Property         | Description                                                                                 | Type                 | Default |
| ---------------- | ------------------------------------------------------------------------------------------- | -------------------- | ------- |
| url              | 接受一个异步请求函数，Table内部会自动接管状态（包括发起请求、分页参数等）                   | Promise函数          | -       |
| columns          | 配置列表项                                                                                  | 与官方API一致        | -       |
| hiddenFilter     | 是否展示Table上面的筛选项组件                                                               | Boolean              | -       |
| tableActions     | 自定义action slot（需要在columns中指定`key: 'action'`）                                     | ref/reactive类型数组 | -       |
| button           | 筛选组件中的独立按钮（如：新增用户）                                                        | ref/reactive类型对象 | -       |
| items            | 筛选组件中的表单项（如：选择角色、搜索名称，会自动生成查询按钮，并接管到Table中的参数状态） | ref/reactive类型数组 | -       |
| tableFilterModel | 筛选组件中的表单项数据模型（配合items使用，为了确定key）                                    | ref/reactive类型对象 | -       |

```html
<template>
  <Table
    ref="ELRef"
    :url="fetchApi.list"
    :columns="columns"
    :actions="tableActions"
    :button="tableFilterButton"
    :items="tableFilterItems"
    :model="tableFilterModel"
  />
</template>
```

使用ref调用Table提供的方法API：

| Property | Description                                                                                  | Type           | Default |
| -------- | -------------------------------------------------------------------------------------------- | -------------- | ------- |
| refresh  | 不接受参数，使用当前的参数发起更新请求（在新增或删除、修改一条数据后，调用该方法进行列表更新 | ()=>void       | -       |
| run      | 接受参数，当需要与自定义参数合并时，并发起新的请求，使用此方                                 | (params)=>void | -       |

```js
const refresh = () => ELRef.value?.refresh();
// const run = (args) => ELRef.value.run(args); 
```

### 特别说明

`config/vite/plugin/mock.ts` 中的 `configMockPlugin` 方法，属性`prodEnabled` 在生产环境一定要关闭，不然会把大量的mock代码，如fakerjs中的一些源码打包进构建包内。

**本项目这里为了做演示，是手动开启了的，为了能在线上部署的时候查看mock数据，实际开发中一定注意关闭！！！**
