## 基础
### 基本类型 
 这个没啥好说
 
 ### 对象类型
 使用接口来定义对象的类型
 ```js
 interface Person {
   name: string;
   age: numbaer;
 }
 
 ```
 - 接口一般首字母大写
 - 接口的属性数量必须与对象一致， 可以设置可选属性， 可选属性的含义是该属性可以不存在
 - 只读属性 readonly 
 
 ### 数组的类型
 
 1.  类型 + [] 表示法
 ```js
 const arr: number[] = [1, 2, 3];
 ```
 2. 数组泛型
 ```js
 const arr: Array<number> = [1, 2, 3];
 ```
 
 ### 函数的类型
 函数的输入输出都要做限制
 
 1. 函数声明
 ```js
 function sum(x:number, y:number):number {
   return x + y;
 }
 ```
 - 输入多余参数不允许
 - 可选参数  同接口的可选属性  用 ? 表示
 - 剩余参数  用数组方式表示
 
 2. 用接口定义函数的形状（函数表达式暂时不考虑
 
 
 ### 联合类型
 联合类型（Union Types)表示取值可以为多种类型中一种  用  |  表示
 
  
 ### 类型断言
 手动指定值的类型  语法为   值 as  类型
 这个暂不深入理解
 
 ### 类型推论
 如果没有明确的指定类型，那么 TypeScript 会依照类型推论（Type Inference）的规则推断出一个类型。
 
 ## 进阶
 ### 别名
   类型别名用来给一个类型起个新名字。
   这个蛮有用
   ```js
   type Name  = string
   ```
   
 ###  字符串字面量类型
 字符串字面量类型用来约束取值只能是某几个字符串中的一个 感觉就是枚举
 ```js
 type EventNames = 'click' | 'scroll' | 'mousemove';
 ```
 
 ### 元组 Tuple
 数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象
 
 ```js
 const tom: [string, number] = ['song', 23];
 ```
 
 ### 枚举
 枚举（Enum）类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。
 
 ```js
 enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};
 ```
 很有用  用到时候再深入理解
 
 ### 类
 暂过
 
 ### 泛型
 泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性
 

 
 
 
