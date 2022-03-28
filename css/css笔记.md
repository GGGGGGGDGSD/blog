## CSS的盒子模型
 - css盒子模型由四部分组成 content padding border margin
 - 有两种类型 标准盒子（默认）和IE盒子 通过box-sizing设置 W3c标准盒子 对应content-box， IE盒子对应border-box
 - 无论那种盒子实际大小都是 盒子实际大小等于 content + border + padding 
 - 这两种盒子的主要区别在与content是否包含了padding和border
 - [codeSandbox demo](https://codesandbox.io/s/css-demo-dsto9)
 - 应用 实现一个三角形:原理也是把content设置为零， 设置border的大小来均分撑起盒子， 不想显示的边社会成透明
## bfc
> bfc会渲染为一个完全独立的区域 有以下方式可以触发
 1. float非none值
 2. overflow非visible
 3. display inline-block 以及table-cell
 4. position absolute fixed

## css选择器
- ID 选择器
- 类选择器
- 元素选择器
- 元素属性选择器
- 选择器列表 A, B
- 后代选择器 A B
- 直接子代选择器 A>B
- 一般兄弟选择器 A~B
- 紧邻兄弟选择器 A+B
- 伪类选择器
- 伪元素选择器


1. 等高布局
https://www.cnblogs.com/weiqinl/p/9663596.html

2. 表格居中
text-align: center;
vertical-align: middle;

3. 表格圆角
  表格直接是不能圆角的
  https://stackoverflow.com/questions/628301/css3s-border-radius-property-and-border-collapsecollapse-dont-mix-how-can-i

4. 伪类与伪元素
伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的
伪元素用于创建一些不在文档树中的元素，并为其添加样式
伪元素 ::before ::after ::first-letter ::first-line
2. css3新特性
 圆角 阴影 渐变 transitions(过渡) animations(动画) flex grid  transform 媒体查询 多列布局

3. flex
flex属性是flex-grow flex-shrink flex-basis的简写  默认值是0 1 auto  后两个属性可选

4. 不知宽高垂直居中
  -   flex
  -  absolute + transition