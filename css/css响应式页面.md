## 响应式布局

> 响应式布局的方案有很多中 比如

1. 媒体查询
2. vw
3. flex
4. grid
 
> 都可以 这里我推荐以grid flex为主, grid相对于flex是二维  布局功能更为强大 而且某些场景grid实现很简单  比如最后一排没有排满的九宫格布局


## 响应式排版
> 相对于布局， 排版主要指文字的字体大小 行高 按钮大小  这种比较细节的展示，这种也有几种可选方案

1. vw
2. rem
3. em

主流就是rem

## 响应式图片
```js
img {
  max-width: 100%:
} 
```

## 注意 
1. 既然是响应式 那就不能把尺寸（width height)设置成固定值

## 参考demo
[code sandbox demo](https://codesandbox.io/s/blissful-hooks-rwvl0?file=/src/style/App.scss:436-443)
这个demo能看到一下
1. grid基本多兰布局使用
2. flex各种及基本的对齐使用
3. 图片的响应式
4. 图片文字混搭响应式布局使用

## 相关学习资料
-[响应式设计](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Responsive_Design)
-[写给自己看的display: grid布局教程](https://www.zhangxinxu.com/wordpress/2018/11/display-grid-css-css3/)

