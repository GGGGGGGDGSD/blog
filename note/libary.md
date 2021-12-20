## Print.js
window.print

## redux-form
  这东西有几个特点
  - 界面不用每次都渲染  提高了性能
  1. 支持immutable.js
  2. fieldArray在动态表单处理方便表现很强大 
    提供了selector和action Createtor 相当于redux getState dispatch

  3. 关于验证
  - validate  同步验证
  - asyncValidate 异步验证
  - submit validate 
   只在提交时候的异步验证是没有的，需要自己在提交时候自己实现（formik库也是这样
  validate
   封装的不错 1 与页面分离 2. 每个字段提供了meta对象跟踪错误对象
   异步验证还没怎么体验

  - submit 可以不用默认的表单提交  提供了各种表单提交状态
  - 
  4. 初始化这块也是有的
  5. 对单元测试的友好
  6. 是否支持ts
  7. 是否支持服务器端渲染
  8. 错误提示
  
  ### 再次使用又发现一些新用法
  1. initialValues直接通过props方式传递就可以设置表单的默认值了 
  2. 可以通过normalize处理要存入store的数据的结构 format可以格式化从store到页面要显示的数据格式（https://redux-form.com/8.2.2/docs/api/field.md/
     主要针对显示和存贮到redux值不一样等场景
  3.  这两个属性才是实现嵌套表单初始化的关键配置
      destroyOnUnmount   : false,
      enableReinitialize : true,
  
  3. 嵌套表单formSection

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

## formik

## react-hook-form
1. 设置初始值
  ```js
    const { register, handleSubmit } = useForm({
    defaultValues: {
      firstName: "bill",
      lastName: "luo",
      email: "test@test.com",
      isDeveloper: true
    }
  });
  ```
  [codesandbox](https://codesandbox.io/s/react-hook-form-defaultvalues-wv8c4?file=/src/index.js:146-327)

2. 检测字段是否编辑过 （dirtyFields  
  所有也可以在提交的时候只提交编辑过的字段
  [codesandbox](https://codesandbox.io/s/react-hook-form-formstate-dirty-touched-submitted-forked-wjk0k?file=/src/index.js:411-422)

3. 错误提示
   [codesandbox](https://codesandbox.io/s/react-hook-form-register-with-error-messages-h9m8p?file=/src/index.js:200-212)

4. 多种形式的表单
  - tab form
  - modal form 
  - nest form
  - 分多步完成的

5. field Array
   [codesandbox](https://react-hook-form.com/api/usefieldarray)

6. 单元测试
   [codesandbox](https://react-hook-form.com/advanced-usage#TestingForm)