- vue2.x data里面都需要this.xx 这样this上面不知道挂载了多少东西都会被打包，而vue3.x组合api只需要引入我们想要的模块，这样tree-shaking打包不会被打包进去。

- 响应式 虚拟dom 模版编译 组件化

- track(target, key) 收集依赖 trigger(target, key, info) 触发更新去执行effect

- effects computeds