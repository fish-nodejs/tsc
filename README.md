# tsc
All the code of TypeScript will be compiled to JS.

We can write a config file `tsconfig.json`

[Offical Doc](https://www.typescriptlang.org/docs/handbook/compiler-options.html)

``` bash
# 创建默认配置文件tsconfig.json
tsc --init
# 除了入口文件和出口文件，其他的一般不用修改默认配置

# 自动监听文件变化
tsc --watch
```
tsc 的编译打包模式有两种
- outDir: 将所有的文件翻译成js文件，如果是想在浏览器中执行，还要用其他打包工具再次打包
- outFile: 直接打包成一个文件。这种情况下就是直接把不同的文件翻译拼接在一起。它们是共享一个命名空间的，而不是通过文件来划分模块，所以非常容易导致命名冲突，这时候可以使用namespace来手动模块化代码。tsc在打包的时候回把它们用闭包的方式让它们自己玩！！

## compiler
- tsc 启动时会尝试在当前问价夹寻找tsconfig.json 作为配置文件，就用默认机制，不要修改。
- 它启动的文件夹就是 rootDir
- 默认配置会将rootDir下的所有ts文件编译成js文件，放在和源文件平级的目录
- 这样很揉乱，可以通过 --outDir: './dist'指明输出文件夹。输入目录结构和rootDir相同
- 上述的做法会有一个遗憾，如果源代码放在 './src/' ,输出文件就是'./dist/src'不美观
- 可以给rootDir 设定为 './src' 解决这个问题
- 但是如果./src 之外还有.ts文件，这种指定就会失效。
- 所以懂了，真的烦躁

## --lib
添加的一些polyfill

## global
现在才明白了，namespace 以及 全局检查 变量名冲突，都是为了将项目打包成
一个文件给浏览器用的副产品，如果我们把ts代码直接翻译成js，再通过
webpack之类的工具打包，就不用考虑这些了。

## vscode
- tslint
为甚tslint不管用？故意写错的类型都不提示，编译的时候才出问题？
slimujiba