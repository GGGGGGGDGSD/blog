# SVG 资源
1. [SVG 教程 MDN](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial)
2. [SVG Properties and CSS](https://css-tricks.com/svg-properties-and-css/)

# 基本

## 一些重要属性
1. viewBox
2. preserveAspectRatio
3. fill & stroke
## 坐标系统
 坐标系统是：以页面的左上角为 (0,0) 坐标点，坐标以像素为单位，x 轴正方向是向右，y 轴正方向是向下。

## 基本图形
 rect circle ellipse line path polyline polygon
 [<path>](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Paths)元素是 SVG基本形状中最强大的一个

## 着色（fill & stroke
1. 类似html里面的background-color 和border
2. 可以通过 CSS 来样式化填充和描边( 表现属性)
3. SVG 规范将属性区分成 properties 和其他 attributes，前者是可以用 CSS 设置的，后者不能。

## 渐变
 暂时不用

## Patterns
## Texts

## 剪切和遮罩

```html
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <clipPath id="cut-off-bottom">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
  </defs>

  <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
</svg>
```

## SVG 相关的单元测试
```js
```