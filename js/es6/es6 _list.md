### ES6
- let const
- 魔板字符串
- 解构赋值
- 新的基本数据类型 symbol bigInt
- 新的迭代结构  map 和 set  weakMap  weakSet 
- 遍历迭代结构  for of
- proxy和reflect
- promise
- genetator
- async await
- class
- module
- 箭头函数
- math + number + string + array + object APIs

[参考](https://github.com/lukehoban/es6features#readme)

=====
module

1. 无论是否声明了 strict mode，导入的模块都运行在严格模式下
2. import 语句只能在声明了 type="module" 的 script 的标签中使用
3. 静态导入（方便应用tree shaking和静态代码分析