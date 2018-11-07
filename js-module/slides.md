---
theme: 'blood'
---

## 简单介绍JS模块

---

- 如有疑问，请随时提
- 如有错漏，请随时怼（轻）

---

## 前情提要

> 如何写一个兼容各种模块规范的库?

- 用esm写，利用babel输出不同规范的模块

---

## 问题来了

- 为什么js会有模块规范？
- 为什么js会有很多种模块规范？
- 有哪些模块规范，分别有哪些实现？它们是怎么来的？各有什么特点？
- 我们现在是怎么使用模块的？
- 怎么写一个兼容各种模块规范的库？

---

## 为什么js会有模块规范？

> “js是世界上最好的语言”

- 可读
- 可维护
- 可重用
- 但是一开始没有模块规范

=> function 作为抽象
=> IIFE 闭包隔离作用域
=> 输出对象

问题
=> 命名空间污染
=> 依赖关系不明确 => 依靠前后顺序

---

## 为什么js会有多种模块规范？

> 学学历史
- 正如在class语法糖之前大家实现OOP的写法五花八门，模块化也是
- 上述例子的不同模块化版本
- IIFE
- ==> Dependecy Injection

---

## 有哪些模块规范？

- CommonJS
- AMD / CMD
- UMD
- ES module 

## CommonJS

> 以前叫ServerJS
- 2009
- 基于文件的模块系统
- 在nodejs里首先实现并普及
- 例子

---

## AMD

- Asynchronous Module Definition(异步模块) - 2011
- https://github.com/amdjs/amdjs-api/blob/master/AMD.md
- dojo
- angularJS - 2010
- requirejs - 2012
- 依赖函数表达式

---

## AMD

- 依赖注入/依赖前置
- 例子
> keywords: 异步, 依赖注入

---

## CMD

> SeaJS: 我的接口文档就是规范
- 依赖就近
- https://github.com/seajs/seajs/issues/242
- 和amd最大的不同是模块执行的机制 -> 都是异步加载，cmd延迟执行

---

## UMD

> Compatibility...

- 其实就是探针/if

## ES Modules

> 俱往矣...

- 大家都熟悉
- named export、 default export

> keyword: 静态分析 - 打包工具

https://medium.com/sungthecoder/javascript-module-module-loader-module-bundler-es6-module-confused-yet-6343510e7bde

http://2ality.com/2014/09/es6-modules-final.html

例子
https://gist.github.com/branneman/558ef3a37ffd58ea004e00db5b201677

---

## 模块机制的几个关键点

- 模块是啥？ref or copy？
- 循环引用

---

## 现在我们是怎么用的？

> 通过打包工具

- bundler: browserify, webpack, rollup
- nodejs能否支持esm？
  - http://2ality.com/2017/05/es-module-specifiers.html
  - http://2ality.com/2017/09/native-esm-node.html
  - .esm
  - 需要metadata - 可能两个都有
- webpack构建出来是什么样的？


---

## 怎么写一个兼容各种模块规范的库？
- https://medium.com/@kelin2025/so-you-wanna-use-es6-modules-714f48b3a953

---

## References

https://ponyfoo.com/articles/brief-history-of-modularity
https://www.jianshu.com/p/09ffac7a3b2c
https://github.com/seajs/seajs/issues/277
https://juejin.im/post/5b6c222a6fb9a04fde5af4ee

---

## Q & A

---

<!-- ## 留坑

- Rollup 模块机制
- webpack 分包加载实现？
- 。。。 -->

---

## 谢谢

---


TODO：

1. md2revealjs
2. 整理思路和讲稿
3. 自己弄清楚 - 不同规范的实现及特点、区别
4. 准备例子 - 各种模块、webpack、rollup、一个模块
5. rehearsal - 演练时间