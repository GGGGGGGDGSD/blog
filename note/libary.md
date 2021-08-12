## Print.js
window.print

## redux-form
  这东西有几个特点
  - 界面不用每次都渲染  提高了性能
  - 支持immutable.js
  - fieldArray在动态表单处理方便表现很强大 
  提供了selector和action Createtor 相当于redux getState dispatch

  - 关于验证
  - validate  同步验证
  - asyncValidate 异步验证
  - submit validate 
   只在提交时候的异步验证是没有的，需要自己在提交时候自己实现（formik库也是这样
  validate
   封装的不错 1 与页面分离 2. 每个字段提供了meta对象跟踪错误对象
   异步验证还没怎么体验

  - submit 可以不用默认的表单提交  提供了各种表单提交状态
  - 初始化这块也是有的
app
  ### 缺点  
  - 这东西是全局的的状态

  Formik似乎很不错（https://formik.org/)
  思考：表单这部分确实可以值得尝试formik 包括他的验证都值得借鉴

## immtable.js
  优势
  - 避免副作用
  - 节省内存 （采用了结构共享机制）
  - 方便回溯 
  https://github.com/redux-form/redux-form/issues/2366

  immutable.js最佳实践
  https://doc.codingdict.com/redux/recipes/UsingImmutableJS/

  ### OrderMap
   - merge 这个使用比较多 合并两个对象并且保证顺序


  ## forEach
    forEach不仅用于List, 也可以是map
    ```js
    forEach(
    sideEffect: (value: V, key: K, iter: this) => any,
    context?: any
    ): number
    ```

## react-tabs
1. 自定制性比较强
2. 可以设置是否强制渲染每个Tab（注意）forceRenderTabPanel forceRender 
   比如使用redux-form 中 FieldArray 就需要forceRenderTabPanel设置为true这样才不会在每次切换时候渲染

## react-select
还未深度使用，不过看介绍自定制性也是很强


## moment
就我们项目而言 完全没必要使用moment这么重型的时间处理库  甚至大部分的应用都不需要
dayjs已经够用了
