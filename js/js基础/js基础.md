

## 参考
- Javascript忍者秘籍
### 类型检测
- typeof 只能检测基本类型
- Object.prototype.toString.call()
- instanceOf 检测应用类型

### 数组

## 面向对象与原型
1. 对象是属性的集合
2. 对象的复用
3. new 创建可复用的对象  继承是复用已有的对象
4. 原型继承
   > 把一个对象的实例作为另一个对象的原型
5. 原型继承的缺点
   1. 不能实现实例的动态传参 所以这一步使用new构造函数实现
   2. constructor容易被修改（可以通过Object.defineProperty 设置constructor的configurable属性实现
   3. 原型也容易被动态修改（这就是js为什么叫做动态基于原型的语言）
   
6. 原型 原型链 与继承
   instance.__proto__ instance.constructor.prototype 得到原型
   instance.constructor instance.__proto__.constructor 得到构造函数
   new instance.constructor() new instance.__proto__.constructor() 得到新的实例


   1. 
7. 对象的访问控制
  > getter  setter Object.defineProperty proxy

8. instanceof
  > 检测右边的原型是否在左边对象的原型链上
## 函数

### 函数定义
 - 函数声明式
 - 函数表达式
 
 > 区别：函数声明式会提升函数
 
### 函数调用
 - 作为函数
 - 作为对象方法
 - 作为构造函数
 - 通过call() 和 apply()
 - 生成器函数
 
 #### this 到底是什么
 > js区分定义作用域和执行作用域，这里执行作用域就是我们所说的this, 即调用当前函数的对象， 根据上面四种调用方式而不同
 
 #### 那有时我想改变这个this, 有时我又想保证这个this不变， 怎么办
 > 改变this  那就是我们的call() apply() 出场了
 > 绑定this  那自然是我们的bind  以可以使用箭头函数
 
 #### 那apply call bind 是如何实现的 我能实现一个？
 - todo
 
 ### 函数参数
  - 实参列表 arguments是一个类数组  es6有了剩余参数是一个数组
  
  #### js是通过位置(顺序）传参， 如何实现关键词传参(参考python)
  > 没错 我们可以传一个key value 形式的对象作为参数来实现
  
  ### js 如何校验传入参数的类型
  > 你居然不知道js是弱类型
  
  ### 作为值的函数
   - 函数作为一个变量
   - 函数作为一个参数
   - 函数作为一个返回值
   
   > 一句话 谁让我是js的一等公民呢
   
  ### 函数对象
  - 没错，函数只是一种特殊对象，也有自己属性和方法
  - 属性  length  prototype
  - 方法 call() apply() bind()
  - 更牛逼的是我们还可以自定义属性和方法
  
  #### 想象一下这样一个题  fn.next() 输出1  每次输出头叠加1 
  - todo
 
 
  ### 闭包(经典问题来了)
  -  调用函数时的作用域链和定义函数时的作用域链不是同一个作用域就是闭包
  - 关键时理解词法作用域， 变量作用域  作用域链
  
  #### 闭包的特征是啥  能干啥
   > 访问内部变量  变量持久化
   > 实现私有变量  模块化
   
  #### 有那些方式实现私有变量？
   
  ### 函数式编程
    - 出函数 无副作用
    - 柯里化
    - 函数组合
    - 递归 尾递归优化
    
   [参考](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/)
 
 
 
 
