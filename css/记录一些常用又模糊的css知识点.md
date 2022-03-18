### 相对模糊的
1. 强制不换行
  white-space: nowrap;

2. flex 下啥情况需要设置width
3. 最近移动端布局 发现用了flex 在设置宽度反而有问题
 https://zhuanlan.zhihu.com/p/269899480

4. ... hover展示全部 添加动画
  https://www.zhangxinxu.com/wordpress/2012/10/more-display-show-hide-tranisition/

5. react-router Link to属性是相对路径 path支持绝对路径

6. 设置字体小于12px
   https://stackoverflow.com/questions/2295095/font-size-12px-doesnt-have-effect-in-google-chrome
   ```css
   transform-origin: left center;
   transform: scale(0.83);
   ```

7. 多个相邻span标签只有有间距 突然发现一个div
  包裹一个img也会出现这种情况(https://stackoverflow.com/questions/7774814/remove-white-space-below-image)
   设置font-size: 0 解决

### 记录一些探索性的（还没还有找到解决方案
1. 能匹配换行的css选择器
2. css 针对自适应的高度可否使用动画
3. 双栏布局 左边一栏高度可否基于右边高度保持一致  右边高度自适应（而且左边高度是远远大于右边的 设置成超出部分滚动）
4. 瀑布流布局