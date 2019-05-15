# TypeScript
## 简介
TypeScript 是 JavaScript 的一个超集，主要提供了类型系统和对 ES6 的支持，它可以编译成纯 JavaScript。
TypeScript 最大的优势便是增强了编辑器和 IDE 的功能，包括代码补全、接口提示、跳转到定义、重构等。
#### 安装
```js
$ npm install -g typescript
```
#### 编译
```js
$ tsc hello.ts
```
我们约定使用 TypeScript 编写的文件以 .ts 为后缀，用 TypeScript 编写 React 时，以 .tsx 为后缀。
TypeScript 只会进行静态检查，如果发现有错误，编译的时候就会报错。TypeScript 编译的时候即使报错了，还是会生成编译结果，我们仍然可以使用这个编译之后的文件。
## 基础
https://ts.xcatliu.com/basics/primitive-data-types