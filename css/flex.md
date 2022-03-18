1. 重点理解flex主轴的概率  以及如何修改主轴 
2.  justify-content 绝对在主轴上的对齐方式 并且理解 space-between space-around space-evenly区别


## 理解flex属性
1. 这个简写属性的每个属性值 flex-grow flex-shrink flex-basis  对应默认值是 0 1 auto
2. flex建议使用常用的缩写 因为单值属性所对应的flex计算值根据开发者日常最常用的使用进行了优化
3. flex对于块级元素大部分不需要设置宽度
4. 常用的缩写
   flex: initial = 0 1 auto
   flex: 0       =  0 1 0%
   flex: none    = 0 0 auto
   flex: 1       = 1 1 0%  // 注意这里是0%
   flex: auto    = 1 1 auto

[参考]（https://www.zhangxinxu.com/wordpress/2020/10/css-flex-0-1-none/）