1 forEach some区别  条件为true是否可以中断遍历
2 const 声明一个引用类型对象  为什么可以修改
3 304的逻辑判断
4 虚拟DOM理解


所有的这些细节  都可以在MDN上面找到答案。


#### 1  创建指定个数数组的快捷方式
```javascript
 let  arr = (new Date(n)).fill('').map((item, index) => index);
 ```

#### 2  获取一个月的天数
> 原理  利用设置天数参数设置为0时返回上个月的最后一天

```javascript
 function getMonthDay(year, month) {
   return (new Date(year, month, 0)).getDate()
 }
 ```
 
 
 #### 3 给一个数组， 求数组中每个元素出现的次数
 > 思路： 通过对象的key值唯一性， 
 
 ```javascript
  var  arr = [1, 2, 2, 3, 4, 4, 4, 4, 5, 5, 5]
  var res = {}
  arr.forEach(scene => {
      if (!res[item]) {
          res[item] = [item];
      } else {
          res[item].push(item)
      }
  })
 ```
 
 #### 5 解构赋值的应用，默认值为什么无效
 > 当且仅当值为undefined时候才会使用默认值
 
 
 #### 6 实现一个es6字符串模板的功能函数


 ### js取消请求

 ### 如何监听请求错误

 import EmptyView from 'shared/components/EmptyView';
    if (!activities.length) return <EmptyView emptyMessage={messages[selfMessages.totalRecordsText.id]} />;


    "<rootDir>/test",
    "<rootDir>/test/specs/index/modules/MyAccount/ViewBookings",

    formatI18n


    /*
## zhichao
1. 还有哪些功能没做
2. 路由是新路由？
3. constomer center不需要展示？
4. unMarked ?


## vd
1. 移动端filter布局？

## new
1. 跳转链接是否区分手机端和移动端
2. 时间显示确实开始和结束时间是同一天？
3. attendance没有事件？

1. 排序是没看到请求参数
  原来分页  排序都是在header里面处理（默认值是在reducer那边设置）

## todo
1. 熟悉处理日期的方法
2. 生产相关时间用 getAgencyToday   测试需要

*/

## ANE-138644 ANE-138646
(对于不确定都要主动照相关人员确定，一般来说都是要和以前类似功能保持一致)
1. 各种溢出处理
2. filter相关移动端是否需要title
3.  loading  应该显示完整的文字scroll down to view more，并且要follow 多语言。 现在只有一个loading，也没多语言化。并且位置也没居中显示，跟下边界线都挨着了
4. sort by菜单用 原生组件  responsive view bookings的sort by菜单用的不是手机系统的原生组件 其它我看activity search页面，instructoravailable hours页面的sort b用的都是原生组件
5. reset all  有reset all显示的位置最好也还是一并问下在尾部显示，还是单独显示在下一行
6. bookings time 换行问题  会影响整体布局 如果强制不换行

7. filter多语言
8. roster 时间显示添加空格
9. roster 和 view bookings时间顺序一致
10. facility wording facility link 手机端折行
11. week 大写
12. roster link 文本和roster页面title 文本  统一
13. button 高度和字体大小
14. loading 文本 国际化
15. datePicker 超过一年的处理方案
16. view bookings  移动端入口

1. loading底部间距
2. reset mobile 新的一行
3. sort by菜单用 原生组件
4. datePicker格式跟随AUI Setting
5. 文案溢出： activity name    customer    facility label      facility link
6. 文案不换行： booking time   month/day
7. data-qa-Id
8. filter 后scroll to top window.scrollTo(0, 0);


## 参考
1. 日期组件要考虑格式和 AUI设置  可以参考 paymentdetails  /Users/ysong/project/cui/src/index/modules/MyAccount/PaymentDetails/components/PaymentDetailFilters/DateRange/index.jsx
   相关  Globalize.ANDateFormat  DateRangePicker
2. SortByMenu 手机端使用原生
  参考： ActivitySearchResults/ResultsHeader

3. autoQAid   用户输入或者操作地方都需要添加
4. 参考  /Users/ysong/project/cui/src/index/modules/Activity/Search/automationIds.js