## 基础
### 基本类型 
 这个没啥好说
 
 ### 对象类型
  - 使用接口来定义对象的类型
 ```js
 interface Person {
   name: string;
   age: number;
 }
 ```

 - 使用type

 ```js
 type Person = {
   name: string;
   age: 'number;
 }
 ```
 - 对象的key
  ```js
  interface Map = {
    [key: number]: string;
  }
  ```
 
 - 接口一般首字母大写
 - 接口的属性数量必须与对象一致， 可以设置可选属性， 可选属性的含义是该属性可以不存在
 - 只读属性 readonly 
 - 非空断言使用的是!，表示可以确定某个标识符是有值的

- 对象继承
   ```js
   interface AddressWithUnit extends BasicAddress {
      unit: string;
    }
   ```



 
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
 1. 数字枚举
   ```ts
   enum Direction {
      NORTH,
      SOUTH,
      EAST,
      WEST,
    }

    let dir: Direction = Direction.NORTH;
    // 默认情况下，NORTH 的初始值为 0，其余的成员会从 1 开始自动增长
   ```

  2. 字符串枚举
   ```ts
   enum Direction {
      NORTH = "NORTH",
      SOUTH = "SOUTH",
      EAST = "EAST",
      WEST = "WEST",
    }
    // Direction.NORTH = 'NORTH'
   ```

  3. 常量枚举
   使用 const 关键字修饰的枚举，常量枚举会使用内联语法，不会为枚举类型编译生成任何 JavaScript

   ```ts
   const enum Direction {
      NORTH,
      SOUTH,
      EAST,
      WEST,
    }

    let dir: Direction = Direction.NORTH; // 0
   ```

  4. 异构枚举
   异构枚举的成员值是数字和字符串的混合：
 
 ```js
 enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};
 ```
 很有用  用到时候再深入理解
 
 ### 类
 暂过

 ### 高级类型
 1. intersection types(交叉类型)
 > 交叉类型是将多个类型合并为一个类型。 这让我们可以把现有的多种类型叠加到一起成为一种类型，它包含了所需的所有类型的特性. 大多是在混入（mixins）或其它不适合典型面向对象模型的地方看到交叉类型的使用
 note!! 同名成员为基础的混入后类型为 never（混入失败， 同名成员为非基础的混入后类型为合并后类型（混入成功
 

 1. Union types(联合类型)
  > 联合类型与交叉类型很有关联，但是使用上却完全不同。 偶尔你会遇到这种情况，一个代码库希望传入number或string类型的参数, 联合类型适合于那些值可以为不同类型的情况

 1. 类型保护
   > 类型保护就是一些表达式，它们会在运行时检查以确保在某个作用域里的类型。 

   - 用户自定义类型保护 要定义一个类型保护，我们只要简单地定义一个函数，它的返回值是一个类型谓词
   ```ts
   // pet is Fish就是类型谓词。 谓词为parameterName is Type这种形式，parameterName必须是来自于当前函数签名里的一个参数名
     function isFish(pet: Fish | Bird): pet is Fish {
        return (<Fish>pet).swim !== undefined;
    }
   ```
   - typeof类型保护
   能被识别的只有"number"，"string"，"boolean"或"symbol" 等字符串，表达式不可以

   - instanceof类型保护

 2. 类型别名
   > 类型别名会给一个类型起个新名字。 类型别名有时和接口很像，但是可以作用于原始值，联合类型，元组以及其它任何你需要手写的类型。 起别名不会新建一个类型 - 它创建了一个新名字来引用那个类型

  3. Index types(索引类型)
   - keyof T  索引类型查询操作符
     对于任何类型T，keyof T的结果为T上已知的公共属性名的联合

   - T[K]，索引访问操作符
     注意需要确保类型变量K extends keyof T
     ```ts
       function getProperty<T, K extends keyof T>(o: T, name: K): T[K] {
          return o[name]; // o[name] is of type T[K]
      }
     ```
  4. 映射类型， in
   > 在映射类型里，新类型以相同的形式去转换旧类型里每个属性， 映射类型，就是使用了 PropertyKeys 联合类型的泛型，其中 PropertyKeys 多是通过 keyof 创建，然后循环遍历键名创建一个类型

   ```ts
     type Clone<T> = {
      [K in keyof T]: T[K];
    };
   ```

 
 ### 泛型
  泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性

   ```ts
   function identity <T, U>(value: T, message: U) : T {
    console.log(message);
      return value;
    }

    console.log(identity<Number, string>(68, "Semlinker"));
   ```

  #### 泛型工具类型 对象类型转换
    1. Pick<Type, Keys> 
      注意：只能用来生成类型 不能生成接口

    2. 1. Omit<Type, Keys> 
    3. Partial
      类型中所有选项变为可选（即加上?:)
    
      ```ts
      type Partial<T> = {
        [P in keyof T]?: T[P];
      };
      ```
     
    4. Required
      将类型中所有选项变为必选（去除所有?:）
    5. Exclude(排除)
      注意: Exclude是操作联合类型的

     
     6. Parameters
       Parameters 获取函数的参数类型，将每个参数类型放进一个元组中
      ```ts
        // 语法
        Parameters<typeof 函数名>
      ```
     7. ReturnType
      获取函数返回值类型
     ```ts
       ReturnType<typeof 函数名>
     ```

  ### 类型保卫
  类型保护是可执行运行时检查的一种表达式，用于确保该类型在一定的范围内
  1. in
  2. typeof
  3. instanceof
  4. is

 ## other
 1. 接口与别名的区别
 2. Any与unknown区别
   any 类型的值执行任何操作，而无需事先执行任何形式的检查

 ### ts自我检测
 [type-challenges](https://github.com/type-challenges/type-challenges)
 > 我目前水平 对我来说都挺难



 
 
 
