---
theme: moon
separator: \n---\n
verticalSeparator: \n--\n
---

## vue + typescript 踩坑实践

---

## 声明

- 不完全实践，待继续探索
- 如有问题，请随时问
- 如有错漏，请随时怼

---

## 先说结论

- Vue生态对ts的支持还有很多问题
- 把SFC用ts改造有很多麻烦
- 但用ts还是有(一些)帮助

<!-- - 三种方法
  - Vue.extend
  - vue-class-component / vue-property-decorator
  - 无SFC直接写ts, tsx -->

---

## 正片

---

## 为啥要上ts？

- 类型检查
- 代码提示

---

## vue怎么上ts? - 基础设置

1. .vue文件模块声明
2. vue上挂载的属性/方法
3. 全局变量（可能是一些第三方库引入）

--

## vue怎么上ts? - 组件写法

> vue写ts的障碍主要是SFC
>
> SFC的障碍主要是template和script里的this

- template里的类型暂时没发现解决方案

--

## vue怎么上ts? - 组件写法

[Vue Doc](https://vuejs.org/v2/guide/typescript.html#ad)

1. Vue.extend
2. vue-class-component / vue-property-decorator

--

## 一、Vue.extend

```js
export default Vue.extend({
  ...
})
```

--

## Vue.extend

> 想象很丰满，现实...

- 看起来可以把遗留代码无缝切到ts

--

- 坑1：prop为Array类型时有问题 [#7895](https://github.com/vuejs/vue/issues/7895) [#8421](https://github.com/vuejs/vue/issues/8421)
  - 可以显式声明prop的类型

--

- 坑2：data里的this只能引用到props的属性 [#8721](https://github.com/vuejs/vue/issues/8721)
  - 那就别用了
  - 或者显示声明this

--

- *坑3* 引用了this的方法需要手动定义返回类型（影响computed、methods等） [Vue Doc](https://vuejs.org/v2/guide/typescript.html#Annotating-Return-Types)
  - 这个要改的地方就多了

--

- *坑4* vuex 的 ts 支持很尴尬 [PR #1121](https://github.com/vuejs/vuex/pull/1121)
  - $store是Store\<any>
  - 要手动 声明各种 map 方法/属性的类型
  - 一个借助 createNamespacedHelper 优化 ts 的 PR 没人合 [PR #1121](https://github.com/vuejs/vuex/pull/1121) -->

--

- 坑5：mixins 类型mix不in
  - 借助util方法也行

--

## 结论

Vue 不借助第三方库写 ts 有点操蛋

- 类型基本靠手写，还得各种填坑

---

## 二、vue-class-component + vue-property-decorator

```ts
@Component({})
export default class MyComp extends Vue {
  // properties go in data
  someState: boolean = true
  // methods go in methods
  someMethod() {
    return true
  }
}
```

--

## 问题

- props, watch

--

## vue-property-decorator

- @Prop()
- @Watch()
- @Emit()
- ...

--

## vuex map 过来的类型

目前除了手动定义我还没找到没啥办法

- 期待[PR #1121](https://github.com/vuejs/vuex/pull/1121)

--

## 结论

Vue 借助第三方库写 ts 也挺蛋疼

- 遗留代码要改造的话语法要大范围重写

---

## 三、TSX

- 解决的template不能类型检查的问题
- 不写sfc了，就用jsx写render方法

---

### 番外1：vuex本身咋写ts？

- 可以用Module<ModuleState, RootState>来定义context类型
- 其它我还没研究过

---

### 番外2：lint

- vscode
  - Vetur还不支持tslint
  - Vetur会对vue文件跑 eslint => 有一些错误报错(ts关键字等)
- pipeline
  - 怎么对vue文件跑lint？(部分eslint，部分tslint) - 我也没研究过

---

## 总结: 现在咋用？

- 新需求可以用 vue-class-component + decorator 来尝试
- store可以加点类型
- 有志之士可以试着去解决上述提到的各种问题

---

## 未来？

Vue 3+ ？
