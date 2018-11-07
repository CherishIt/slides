---
theme: blood
separator: \n---\n
verticalSeparator: \n--\n
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
- 有哪些模块规范?
- 我们现在是怎么进行模块化开发的？

---

## 为什么js会有模块规范？

> “js是世界上最好的语言”

- 但是却没有官方的模块支持 <!-- .element: class="fragment" data-fragment-index="1" -->

--

## 模块化的好处

- 隔离
- 可维护
- 可重用

---

## 古代js模块实践

--

### script标签

```html
<script>
  function add(a, b) {
    return a + b
  }
</script>
<script>
  const $container = document.getElementById('container')
  $container.innerText = add(1, 2)
</script>
```

--

### IIFE

```html
<script>
  function add(a, b) {
    return a + b
  }
</script>
<script>
  (function() {
    const $container = document.getElementById('container')
    $container.innerText = add(1, 2)
  })()
</script>
```

--

```html
<script>
  const Util = (function() {
    ...
    function add(a, b) {
      return a + b
    }
    return { add }
  })()
</script>
<script>
  (function() {
    const $container = document.getElementById('container')
    $container.innerText = Util.add(1, 2)
  })()
</script>
```

--

```html
<script>
  const Util = {}
  (function(U) {
    function add(a, b) {
      return a + b
    }
    U.add = add
  })(Util)
</script>
<script>
  (function(U) {
    const $container = document.getElementById('container')
    $container.innerText = U.add(1, 2)
  })(Util)
</script>
```

---

## 近代js模块规范

- CommonJS
- AMD / CMD
- UMD
- ...

--

## CommonJS - 2009

> 一开始叫ServerJS
- nodejs里实现并普及
- 每个文件是一个模块
- 通过require来引用其他模块 - 同步执行文件/读取缓存
- 模块的输出是module.exports

--

## AMD

- Asynchronous Module Definition(异步模块) - 2011
- https://github.com/amdjs/amdjs-api/blob/master/AMD.md
- 怎么在浏览器里方便地使用模块？

--

## CMD

- https://github.com/seajs/seajs/issues/242

```js
define(function(require, exports, module) {
  const add = require('add')
})
```

--

## UMD

- https://github.com/umdjs/umd
- [dazhaohu](https://github.com/sjy/dazhaohu/blob/master/dist/dzh.js)

---

## ES Modules

> 俱往矣...

- named/default import/export

```js
export default function () {}
export const a = 1
import fun, { a } from 'xxx'
```

--

- 兼容同步/异步加载
- 静态语法
  - 编译时就能知道模块间依赖关系
  - const xxx = require(isProd ? 'xxx' : 'xxx-dev')
- 倾向于default export
- 能处理循环依赖

---

## 现在我们是怎么用的？

> 通过打包工具

- webpack

--

- 每次要调用webpack_require
- 每次要访问modules

--

## Scope Hoisting

- https://rollupjs.org/repl

---

## 未来？

- 浏览器原生支持？

---

## References

https://ponyfoo.com/articles/brief-history-of-modularity
https://www.jianshu.com/p/09ffac7a3b2c
https://github.com/seajs/seajs/issues/277
https://juejin.im/post/5b6c222a6fb9a04fde5af4ee
http://www.ruanyifeng.com/blog/2015/11/circular-dependency.html
https://medium.com/sungthecoder/javascript-module-module-loader-module-bundler-es6-module-confused-yet-6343510e7bde
http://2ality.com/2014/09/es6-modules-final.html
https://zhuanlan.zhihu.com/p/25046637
https://medium.com/webpack/brief-introduction-to-scope-hoisting-in-webpack-8435084c171f
https://juejin.im/post/590a990a5c497d005852cf61
https://zhuanlan.zhihu.com/p/26559480

---

## Q & A

---

## 谢谢

---

