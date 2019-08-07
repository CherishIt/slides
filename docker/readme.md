---
theme: sky
separator: \n---\n
verticalSeparator: \n--\n
---

# Docker 初探

---

## 内容

- Docker是什么？
- Docker怎么用？
- Docker的原理
- 其它

---

## 啥是Docker

- Docker公司(原dotCloud)
- Docker公司的容器化产品(Docker-EE, Docker-CE等)
- Docker公司开源的docker项目([moby](https://github.com/moby/moby))

--

## 啥是容器

- 打包了应用的运行环境、不需要各种配置
- 开箱即用
- 灵活、轻量、可替换、可扩展

--

<!-- .slide: data-background="./docker-vm.png" -->

--

## 容器 vs 虚拟机

- 虚拟机
  - 需要Hypervisor做硬件虚拟化
  - 需要安装完整的操作系统
  - 有性能、空间损耗
  - 完全隔离
- Docker
  - 直接使用宿主机操作系统内核
  - 轻量
  - 通过linux的一些特性实现隔离与限制, 隔离不彻底

--

## 啥都不管先上手试试

- 打包一个最简单的镜像
- 基于这个镜像run一个容器

--

## 镜像 vs 容器

- 容器是一个运行着的docker镜像

--

## Docker registry

- 管理镜像

--

## Docker架构

--

<!-- .slide: data-background="./docker-arch.png" -->

--

- dockerd - 处理docker请求，管理docker资源
- docker client - 用户和docker交互，把命令交给dockerd处理
- docker objects - 镜像、容器、服务等
- docker registries - 保存docker镜像

---

## docker原理

- Namespace - 运行空间隔离
- Control groups - 资源隔离与限制
- Union FS

--

## Namespace

- namespace是linux创建进程时提供的一个隔离机制

```c
// 创建进程时可以携带namespace参数
clone(main_function, stack_size, SIGCHLD, NULL);
// 使某进程脱离某个ns
unshare()
// 使某进程加入某个ns
setns()
```

--

- UTS namespaces - 进程hostname
- IPC namespaces - 进程间通信
- PID namespaces - 进程的PID
- Mount namespaces - 进程文件系统
- Network namespaces - 网络
- User namespaces - 用户

--

## Cgroups

- 限制一个进程组能够使用的资源上限，包括 CPU、内存、磁盘、带宽等
- 接口是文件系统, 把需要限制的进程pid写入文件tasks

--

## 一个例子

- cpu.cfs_quota_us
- cpu.cfs_period_us
- while :; do :; done &

--

## Union FS

- 把多个不同目录下的文件系统挂载到同一个目录下

--

- 每个运行的docker都有自己的文件系统，那同一个镜像跑多个容器会生成多份文件吗？
- 如果共用镜像文件，一个容器的修改会影响另一个吗？
- 在docker里面修改/编辑文件改的是啥？

--

<!-- .slide: data-background="./docker-fs.png" -->

--

## Docker文件系统分层

- 容器文件系统由多层组成
- 只读层 - ro+wh => readonly + whiteout
- Init层
  - 用户可能会修改一些系统信息
  - /etc/hosts, /etc/resolv.conf等
  - 修改往往只对当前容器有效，这一层不会被提交
- 可读写层 - rw => readwrite
  - 编辑只读层的文件是, 在这一层存储一些增量文件
  - 把只读层`whiteout`掉

--

<!-- .slide: data-background="./docker-vm2.png" -->

--

## docker-compose, swarm, k8s

- 容器编排

---

## 总结

- docker镜像打包了应用的整个运行环境和依赖，开箱即用
- docker的是运用了Linux的一些特性实现了隔离与限制
- 一个docker容器就是一个在隔离环境中运行中的Linux进程

---

References:

- [官方文档](https://docs.docker.com/get-started/)
- CoolShell:
  - [DOCKER基础技术：LINUX NAMESPACE](https://coolshell.cn/articles/17010.html)
  - [DOCKER基础技术：LINUX CGROUP](https://coolshell.cn/articles/17049.html)
  - [DOCKER基础技术：AUFS](https://coolshell.cn/articles/17061.html)
- 极客时间

---
