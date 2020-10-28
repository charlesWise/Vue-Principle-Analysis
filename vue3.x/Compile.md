vue3按需更新 编译时优化

1、写的依然是html，实际执行的是js
2、template => render函数，经典编译原理
3、ast => transform => generate

code => ast => 静态标记 => 生成最终代码执行

### 静态标记，vue2是否也是有静态标记？
编译时优化（灵感来自prepack.io），通过位运算做的标记patchFlag，react事件系统也用到位运算

vue2也是有静态标记，只能标记全量的静态，比如v-if里面的就都视为动态标记就不会去标记，再如：
<p id="xx" style="color: red">{{name}}</p>这个节点只有child是动态vue2也会去diff id、style；而vue3只会去diff children name，做的更细致些只会diff动态的节点

compile => baseCompile => baseParse => template => ast 然后针对vue3逻辑的一些优化，比如说v-model v-on v-for 静态提升， atransform 之后 generate 生成可执行的代码

### vdom
传统的vdom的diff不管是静态还是动态的都会去diff一遍，其实我们需要diff的是动态节点。这样就会浪费时间，当大于16.6ms的时候就会卡顿，所以vue3有了静态标记减少diff，静态标记只diff动态的节点。包括react15也是这样之后react16，react fiber走了另外一条路，并没有减少什么工作量只是把宏观的树变成了链表，链表特点可中断，在这个diff当中如果一旦达到16.6ms的阈值就会把控制权还给浏览器去进行你的动画下一帧再还给我，我继续执行我上一帧没有完成的diff。

### block tree 区块树
可以理解解决v-if v-for动态节点内部静态节点所存在的专门结构，把正tree分成很多的block这个block把内部动态节点都维护在单独的数组里面，这样我们就避免了很多的递归

Q：vue3为什么没有利用idle时间切片：
A：原因是因为它的切片已经足够小，每个任务都很小，不太需要时间切片。