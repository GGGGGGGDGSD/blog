最近发现平时scss使用率是最高的 但是使用的特性却把不很多  说明还需要提高掌握

## 特征
1. 变量、嵌套 (nesting)、混合 (mixins) 等功能
2. 函数进行颜色值与属性值的运算
3. 控制指令 (control directives)等高级功能
## 基本
1. 变量 $size: 80px;

2. sass文件
  sass局部文件的文件名以下划线开头，sass就不会在编译时单独编译这个文件输出css，而只把这个文件用作导入

3. 默认变量值
  ```scss
  $fancybox-width: 400px !default;
  .fancybox {
    width: $fancybox-width;
  }
  ```
4. mixin
```scss
// 内部mixin 不会到处套其他问题  _ 开头
@mixin _fill-large-svg-color($bgColor, $color) {
  path:first-child {
    fill: $bgColor;
    stroke: $bgColor;
  }
  path:not(:first-child) {
    fill: $color;
    stroke: $color;
  }
}

// 导出复用
/*
1. 参数
2. 可在内部使用&引用父选择器
3. @use 'mixin'， @include mixin.styling;  引入使用
4. 考虑些写单元测试
*/
@mixin styling {
  @include _fill-large-svg-color(color-vars.$white, color-vars.$white);

  &.spinner-light {
    @include _fill-small-svg-color(color-vars.$primary-100);
  }

  &.spinner-dark {
    @include _fill-small-svg-color(color-vars.$white);
  }

  &.spinner-super {
    @include _fill-large-svg-color(color-vars.$grey-60, color-vars.$brand-105);
  }

  &.spinner-primary {
    @include _fill-large-svg-color(color-vars.$grey-60, color-vars.$primary-90);
  }
}
```
5. 


