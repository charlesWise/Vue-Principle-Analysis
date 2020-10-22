- Virtual DOM如何工作的？
```
Q：什么是VDOM？
A：是由普通JS对象来描述DOM对象，因为不是真实的DOM对象。

Q：为什么使用VDOM？
A：手动操作DOM比较麻烦，还需要考虑浏览器兼容性，为了简化复杂操作出现了MVVM解决视图和状态同步问题，但是没有解决跟踪状态变化的问题，于是有了VDOM的出现，当我们的状态改变时不需要立马更新DOM只需要创建一个虚拟树来描述DOM，VDOM内部将弄清楚如何有效（diff）更新DOM。总结：VDOM可以维护程序的状态，跟踪上一次的状态，通过比较前后两次状态的差异更新真实DOM。
```

- vue2.x内部使用VDOM就是改造的Snabbdom
```
Snabbdom基本使用
npm i parcel-bundler

h函数：ts的重载函数生成vnode
  - vnode虚拟节点
```

- vnode是如何渲染成真实dom的？
```
patch(oldVnode, newVnode)打补丁，把新节点中变化的内容渲染到真实DOM，最后返回新节点作为下一次处理的旧节点；对比新旧Vnode是否相同节点（节点的key和sel（span、div）相同）；如果不是相同节点，删除之前的内容，重新渲染；如果是相同节点，找节点的差异并更新DOM，再判断新的Vnode是否是text，如果是并且和oldVnode的text不同，直接更新文本内容；如果新的Vnode有children，判断子节点是否有变化，判断子节点的过程使用的就是diff算法；diff过程只进行同层级比较。
```

```
init()返回patch()函数即高阶函数，patch函数把vnode渲染成真实dom，并返回vnode

```