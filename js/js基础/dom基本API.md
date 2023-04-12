# DOM

# 为什么需要重新学习这部分
  主要还是使用的需要，目前使用testing-library/react写单元测试会涉及到  还有使用typescript时候也需要了解对应的dom类型 这是目前主要原因 

## Node(这部分其实react源码里面使用的很多)

> Node 是一个接口，各种类型的 DOM API 对象会从这个接口继承

1. Node type. 
  > elementNode textNode attributeNode documentNode commentsNode and so on

2. node 关系
  > parentNode childNodes firstNode lastNode previousSibling nextSibling

2. 常见node属性


## 节点选择
1. querySelector querySelectorAll, getElementById getElementByClassName getElementByTagName

2. createElement appendChild
```js
const newElement = document.createElement('div');
newElement.textContent = 'test';
document.body.appendChild(newElement);
```
3. 节点操作
   node.appendChild() node.removeChild() node.replaceChild()

4. 属性操作
  element.setAttribute() element.removeAttribute() element.getAttribute(attrName) element.hasAttribute(attrName)

5. dom 事件
    element.addEventListener(type, listener, [, options])
    element.removeEventListener(type, listener, [, options])
    document.createEvent() element.dispatchEvent(event)

6. 元素样式尺寸
   window.getComputedStyle(elem)
   elem.getBoundingClientRect()

7. 利用classList 操作 className 
   
## 参考资源
- [常用DOM的API总结](https://zhuanlan.zhihu.com/p/130298762)
## other
1. shadow dom
2. template 标签