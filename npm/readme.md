---
theme: blood
separator: \n---\n
verticalSeparator: \n--\n
---

# 讲讲npm

---

## 讲啥

- npm是啥
- 一些基础知识
- npm vs yarn vs pnpm
- private npm

---

## npm是啥

--

- Node Package Manager
- Node.js官方捆绑
- 包管理工具
  - 注册中心
  - 安装、配置、升级、删除包
  - 免去手动安装和升级的痛苦
<!-- 不同平台/语言的包管理工具 -->
- 例如：homebrew, apt-get, ruby gem, python pip, ...
<!-- App store: 应用级别, Github: 代码片段 -->
- 又如：App Store, Github, ...

--

### 问题

如果要你开发一个 Package Manager 你会怎么设计？

--

### Client/Server

- 一个用来管理包的服务器
  - 存储已发布的包 和 相关信息
  - 提供接口来查询、发布包
- 一个用户交互界面（cli）
  - 通过接口与服务器交互
  - 执行 安装、发布 等操作

--

### npm

- [npm cli](https://github.com/npm/cli)
- [npm website](https://npmjs.com)
- [npm registry](https://registry.npmjs.org/)

---

### npm的一些基础知识

<!-- package的描述文件metadata -->
- package.json
- version
  - semver: major.minor.patch (~ ^ > = < x *)
  - dist-tags: latest
<!-- shrinkwrap, package-lock -->
- lock files
  - shrinkwrap, package-lock
<!-- 本地安装 ./node_modules, 全局安装在node的安装目录下 -->
- local vs global

--

### npm的一些基础知识

<!-- --production -->
- dependencies, devDependencies, peer/optional/bundle
<!-- npm 相关的一些配置，可以通过命令设置，会被写到.npmrc文件里 -->
<!-- yarn --verbose -->
- config - npmrc
  - cli > project > user > global > builtin
<!-- 默认私有 -->
- scope - @xxx/
<!-- 预置 & hooks -->
- scripts

---

## npm vs yarn vs pnpm - cli

- speed
- liability

--

### yarn

<!-- 本地cache vs npm cache 也不会用 -->
- cache && offline mode
- lockfile
- npm@5
<!-- yarn why & yarn update --interactive -->

--

### pnpm

- global package store - 省空间
- hard link + symlink
- node_module tree

---

## private npm - registry

- 为啥需要私有npm？

--

### 我们的私有npm是怎么搭的

- cnpm

--

## References

- [npm docs](https://docs.npmjs.com)
- [Package Manager Wiki](https://en.wikipedia.org/wiki/Package_manager)
- [npm yarn pnpm](https://smddzcy.com/posts/2019-05-19/npm-vs-yarn-vs-pnpm-package-manager-comparison)
- [pnpm](https://github.com/pnpm/pnpm)
- [yarn issue #1761](https://github.com/yarnpkg/yarn/issues/1761)
- [cnpm](https://github.com/cnpm/cnpmjs.org)
- [The Economics of open source](https://2019.jsconf.eu/c-j-silverio/the-economics-of-open-source.html)

---

## Others

<!-- - install是个什么样的过程? -->

---
