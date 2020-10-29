分层：
  runtime-core 复制和平台无关到事情（只标记新增 删除节点）
  runtime-dom 实现浏览器增删改查
  
  别的平台，都可以基于runtime-core实现自己到一套custom renderer 自定义渲染器

  runtime-mp 小程序
  runtime-webgl

vdom diff
  预判机制，当预判没有匹配就会实行最长递增子序列，新增 移动 删除元素操作 贪心+二分算法