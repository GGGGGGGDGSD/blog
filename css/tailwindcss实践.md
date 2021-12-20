<!-- https://www.tailwindcss.cn/docs/padding -->
1. 总体来说我还是看好tailwind 原因几
   - 在熟悉各种类的基础上和手写css一样
   - 各种类是可以复用的最小单单位  意味着最终的css并不会很大 因为都是复用各种基本类
  
2. 一些遇到的问题
  - 如何精确的使用项目中的颜色值
   目前的解决方式是自定义了 除了颜色值 包括其他很多都需要采用这种自定义的方式实现 这也是官方推荐的方式

3. 类名只能作用与当前的element上
    比如 input:focus  ~label 这种实现
  [参考实现方式](https://notiz.dev/blog/floating-form-field-with-tailwindcss)
