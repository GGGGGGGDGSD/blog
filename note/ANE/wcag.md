

##  related document
- Aria Mdn https://developer.mozilla.org/zh-CN/docs/Web/Accessibility/ARIA
- Web内容无障碍指南 [WCAG](https://www.w3.org/Translations/WCAG20-zh/WCAG20-zh-20141009/)


## ticket 
Wcag

1. Wave
   使用这个插件来检测页面查看是否有error以及对比度问题
   disable状态下对比度问题不用修复
2. 使用AMP插件来检测页面问题
   1. 只处理大于等于7的  可以高亮查看元素，
3. 键盘事件问题
  1. 添加键盘事件
  2. Tab访问顺序问题
    1. 严格按照文档流的顺序
    2. 如果某些文档流顺序正常 但是focus顺序有问题  一般都是这里有focus的强制处理导致
    3. focus的强制处理来保证focus顺序，同时也可以考虑是否把tabIndex=-1让键盘不能访问
4. 读屏
   1. 按照 [这里](http://ux.active.com/wireframes/ANE/WCAG%20Guideline%202.0/#p=1_0_wcag_keyboard_definition_for_component_in_cui_&id=wpswwi&g=12) 来设置内容


## aria 相关属性

### aria role

### aria state

1. aria-live
   提供了一种以编程方式显现动态内容更改的方法  可能的设置：off, polite or assertive,
   常用使用场景： 各种表单错误 全局通知等
[参考](https://developer.mozilla.org/zh-CN/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)

2. aria-invalid
   The aria-invalid attribute can be used with any typical HTML form element, and is not limited to elements that have an ARIA role assigned.

   attribute is used to indicate that the value entered into an input field is not in a format or a value the application will accept. This may include formats such as email addresses or telephone numbers. aria-invalid can also be used to indicate that a required field is empty.

3. progressbar aria-valuemin aria-valuemax aria-valuenow

4. voiceOver
 按下 Control 键 来控制暂停或者继续
 Copy a phrase to the Clipboard (or Pasteboard): Press VO-Shift-C.
  
1. jaws
  insert + space then press H


### 技巧
1.  如果做responsive wcag , 最好先找到这个ticket对应的responsive  ticket  这样能快速的知道responsive的修改
   比如 ANE-143913 （wcag) => ANE-121987(https://gitlab.dev.activenetwork.com/ActiveNet/cui/-/commit/452bd69504766ac07f36a6af1f90ab37e6297f1b)



## todo
1. 为啥这个写法有问题(onKeyDown 不能被调用)
   const instance = component.instance();
    // const onKeyDown = jest.spyOn(instance, 'onKeyDown');
    const item = component.find('.home-module__desc-icon').at(moduleIndex);
    console.log('===44====================== ~ it ~ item', item)
    item.simulate('keydown', {
      stopPropagation: jest.fn(),
      preventDefault: jest.fn(),
      keyCode: KeyCode.ENTER,
      shiftKey: false
    }, moduleIndex);

    // expect(onKeyDown).toBeCalled()

2. expect(onKeyDown).toBeCalled() 和 expect(onKeyDown).toBeCalled 区别

## 具体case
Ensures every form element has a label
需要为表单元素添加 aria-label

time 日期下拉选择框
aria-controls={expanded ? calendarId : undefined}
aria-expanded={expanded}
aria-haspopup="listbox"

TimePicker DatePicker Dropdown




## active/css  wcag
Tag  组件自身样式对比度问题
TagsInput 不支持传递aria相关参数
Input 对比度有点问题
Step indicator 组件自身样式对比度问题
Progress 缺少role aria-label

Alert 组件自身样式对比度问题(不用处理)


## 遇到一些问题 (key: Accessible  on a group of checkbox)
role 为 group 的div标签 checkbox group 如何让读屏器读出required
1. aria-required不能用到role='group'
2. required属性只能用于form标签

目前收集到一些方案
1. required放到label标签上实现 
2. role为combobox
3. fieldset [fieldset MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/fieldset)

reference links
- https://stackoverflow.com/questions/6218494/using-the-html5-required-attribute-for-a-group-of-checkboxes
- https://www.w3.org/TR/2016/WD-wai-aria-practices-1.1-20160317/examples/checkbox/checkbox-2.html
- https://www.w3.org/WAI/tutorials/forms/grouping/
- https://www.a11ymatters.com/pattern/checkbox/
- https://stackoverflow.com/questions/71555672/create-accessible-checkbox-group-with-multiple-descriptions
- https://blog.tenon.io/accessible-validation-of-checkbox-and-radiobutton-groups/

相关参考
- [required MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:required)
- [aria-required MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-required)