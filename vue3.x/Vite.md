- webpack dev server 在启动时，需要选 build 一遍生成 bundle 文件在内存中，再启动 web server，而 build 的过程时需要费很多时间。
- vite 是内部直接启动 web server 并不会先编译所有代码文件。因为vite利用现代浏览器原生支持ESM特性，省掉了对模块对打包；也就是说只有具体去请求这个文件的时候才去编译这个文件。所有这种即使编译体现出：按需编译。
- vite有个子命令optimize，优化依赖就是自动去把代码的第三方模块提前编译出来。

- HMR，vite立即编译当前所修改的文件，而webpack修改某个文件会自动以这个文件为入口重写build一次，所有依赖都会被加载一遍，速度当然会慢。

- vite生产模式打包内部才有rollup完成打包，对于code splitting需求，vite内部采用原生dynamic imports特性实现，所以打包结果还是只能支持现代浏览器，不过好在dynamic-import-polyfill可以运行相对低版本浏览器。

- 核心功能Static Server + Compile + HMR，实现思路：1、将当前项目目录作为静态文件服务器的根目录2、拦截部分文件请求（处理代码中import node_modules中的模块、处理vue单文件组件的编译）3、通过websocket实现HMR
