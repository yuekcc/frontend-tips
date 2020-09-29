## js/ts

### 声明变量时使用 es6语法：const、let

es6 又叫 es2015 已经发布 5 年了。es6 最大的改进是引入了 const、let 关键字。是时候使用 const、let 了。
在 every green 浏览器更推荐使用 es2015+ 语法。

虽然现在经过 babel/typescript 转换后都是 var，但是在 eslint 中还是相当有意义的。

### 优先使用 const 声明变量

const 关键字的好处是变量声明后，不能被再次赋值可以减少一些错误。

### 变量声明应该尽量初始化。一些初始值：

初始化可以减少 null/undefined 问题。

    - 数值：0
    - 字符串：''
    - boolean：false
    - 数组：[]
    - 对象（hashmap）: {}
    - 对象（object）: null 或具体的初始值

### 外部接口尽量进行“空”判断，除非清楚自己在做什么

一句话：接口数据是不可靠。不是所有人都是面向协议编程。

### 异步编程时优先使用 async/await 语法，这些代码会更清晰

async/await 可以将复杂麻烦的回调改写为简单直接的类似于同步的代码。更方便理解、修改。

### 使用 typescript 而不是 anyscript

写 anyscript 不如直接写 typescript。

### 不要利用 js 的隐式类型转换特性编写代码。写清晰好理解的代码，而不是神代码。

```js
const sum = "1" + 100 - (+new Date()) + "1000A"
```

不是在面试不是在考试，不需要 show 技巧。

### 时常重构代码

最实用的重构是给变量、方法起一个合适的名字。所谓通过代码解释自己，而不是注释，更不是口口相传。

## vue

### 使用 @vue/composition-api 特性

vue2 过度到 vue3 的好东西。

### 非必须不使用 Vue.prototype 挂载对象/方法

@vue/composition-api 提供了 provider/inject 可以很方便使用这个功能。另外就是 @vue/composition-api 中 setup 阶段是不能用 this 的。
是时候放弃 Vue.prototype 挂载对象/方法的习惯了。

### 尽量不使用默认导出（export default）

默认导出无 IDE 的智能提示，也不方便重构

### 自定义的组件导入时，应使用大写 CamelCase

html 原生标签全是小写之母。三方库一般是 el-button 风格。自定义组件 PageHeader 风格。一看就非常明确。

### 组件的 props、event 可以加上前缀。方便区分变量、props、原生事件

思考一个问题 @click 和 原生的 onclick 是同一个事件？与其猜或找文档，不如直接在命名上进行区分。

### 优先使用 template 而不是 render 函数

vue 的 template 中项目构建时会转换为 render 函数。可以自动处理的应该交给机器。template 可以满足 90% 的开发需求。也更为直接。

### 在 template 中，自定义组件使用 CamelCase 风格。ui 库使用其推荐风格。

```html
<PageHeader>
    <el-button>hello</el-button>
</PageHeader>
```

### 组件使用实例注册，而不是全局注册。

大部分情况下，自定义的组件是针对特定业务的，基本上无法复用。可以被多个组件引用而且无具体业务的特性的组件才是公共组件。例如一般 ui 库的基础组件。

### 在 template 中，组件的 props、event 使用 kebab-case。例如

```html
<PageHeader :x-title="'some title'" @x-back="goBack" />
```

### 控制一个组件的代码量。超过 1k 行的组件应该是问题组件。需要考虑拆分。

## css

### 使用局部分样式（scoped）
### 类命名：kebab-case

例：
```scss
.page-title {
    // ...

    & h1 {
        // ...
    }
}
```

### 使用 scss
### 需要全局样式修改的情况下，集中在个样式文件中完成
### 需要样式穿透的，要注意控制影响范围

## 工程

### 文件名原则上应该都使用小写字母、-（中划线）

windows 系统的文件名不区分大小写，linux 系统区分大小写。全小写可以避免一些无谓的问题。前端更习惯使用 - 分割单词。

### 文件名可以加上特别后缀，以区分具体功能。

例如：user.service.ts、validate-user.guard.ts

一些常见的后缀：

- service: 服务
- guard: 路由守卫
- filter: vue 的过滤器
- directive: vue 的自定义指令

### 一个代码文件只用于编写一组紧密相关的函数、组件、一个类，甚至一个函数、常量

控制代码的布局。多人协助时，减少冲突。

### eslint 你值得拥有

js 是动态类型语言。eslint 可以在编写代码时进行一些检查，减少错误。也可以矫正一些不好编程习惯。

### prettier 你值得拥有

prettier 是目前流行的代码格式化工具。用户包括 vue 全家、react 全家，还有 n 多 npm 包。


### 使用 typescript

js 是一种动态类型的编程语言。动态类型语言的特点就是不到最后一刻也是不知道这个变量是什么？里面有什么数据。typescript 减少这方面的问题。

### 全局使用一种或一套命名风格

**不要混搭！风格没有对错，只有统一和不统一之分**。原则上命名风格应该与世界接轨。对项目好也对自己好。

### 只使用一套基础组件库

基础组件库因为涉及大量功能，往往同类型的基础组件库都具有类似的功能。而且经常被全局引用。引用多个基础软件库容易引入奇怪的问题。例如样式覆盖、事件覆盖等。

### 简化导入（import）路径，使用绝对路径导入

```ts
import { formatDateTime } from '@/shared/utils/format-date-time'
import { PageHeader} from '@/components/page-header'
```

工具类直接指定到具体的文件。vue 组件可以先在组件所在目录中建立一个 index.ts 文件，再引用。如上面的例子
目录实际上是这样的：

```
/src
    /components
        /page-header
            /index.ts
            /page-header.vue
```

index.ts 代码：

```ts
import Component from './page-header.vue';
export const PageHeader = Component;
```
page-header.vue 代码：

```vue
<script lang="ts">
export default {
    // ...
    setup() {
        return {

        }
    }
}
</script>

<template>
    <div>
        <slot />
    </div>
</template>
```
