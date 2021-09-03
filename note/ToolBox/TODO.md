## ToolBox接下来要做什么


org district  school admin  只能是其中一个

toolBox 和所有web  mobile端联动测试


## 一些问题
1 webapp 缺少一些功能  比如没有region的school 在web 没有显示school  都统一显示district
2 toolBox也缺少好多功能
3 tooBox 13检查没做

============late
4 tooltip动态渲染
```js
return (
    <Table bordered>
      <thead>
        <tr>
          { tableHeads && tableHeads.map((item) => {
            if (item === 'Audience') {
              return (
                <th key={item}>
                  {item}
                  {'  '}
                  <i id="Audience" className="fas fa-exclamation-circle cursor-pointer" />
                  <Tooltip placement="top" isOpen={tooltipOpen} target="Audience" toggle={toggleTooltip}>
                  {
                    `
                    A/T/S/P = 
                    Administrator/Teacher/Student/Parent
                    `
                  }
                  </Tooltip>
                </th>
              );
            }

            return <th key={item}>{item}</th>;
          })}
        </tr>
      </thead>
      { children }
    </Table>
  );
// 从编辑页面过来报错了 解决方法是添加trigger="hover"（不理解
```



1 school district Takeover done yet
2 send two request (Country Accounts Tab page)

### Users
1 搜索用户到用户详情页 make Admin点击用户成功admin之后再点击remove admin 成功之后按钮显示还是remove admin
2 Delete Account 功能没实现
3 相关搜索中  检索关键词前后的空格没有过滤
4 enterprise account Tab 里面 reset按钮有问题（1 可点击状态逻辑不对  2  居然有两个相同功能的组件）

### Enterprese Acccounts
- Regions Tab数据后端返回总页面数据错误(有时)
- Schools Tab 通过school_id即使id不存在搜索总是返回所有数据



user来源
1 自动注册  手动verified(普通user)
2 count account  onboard 自动 email verified(enterprese user)


## 一些问题 
代码规范  命名

代码问题
分页没有loading动画  以及很多action beginAjaxaction没有 或者是放在页面

## Toast组件问题
 - 控制toast显示的时间居然不是通过传递一个时间参数  而是在自己手动使用setTimeout
 - 控制toast显示的类型的样式（成功  失败）居然是通过类型的后七位字符串作为样式的class来控制


###  重要
1. 还有一门公共考试
2. cypress相关学习
3. collaborator访问其他详情页设计方案（周五下午线上讨论）基于下
  这个得让我想想，我目前初步想法是，就是像page helper那样，建立一个feature helper, 里面存着能访问的功能。如果是collaborator，去那个列表里找

### sprint思考
1. 后端api需要一套规范 比如固定的提示错误的字段


### TBOX track
1 Create A Country Account Modal表单字段没有明显的提示 这会导致创建直接失败而且没有明确失败原因
2 页面有很多

##  838 存在的问题
 这个核心action detailsModalFetch 在SingleMemberCheckListItem组件中还被引用  目前838中不处理了  做个记录



## 每周五PR汇总给张宇
- 需要合并的PR
- 不想要被合并的PR



##  bug list note
956    frontend + backend 后端需要提供一个新的字段和接口
954    backend?
952    backend
942    backend?(需要再验证)
931    backend
894    backend?
877    backend   
870    backend + frontend   需要后端看下official_id与NCES ID处理逻辑
862    backend    后端做特殊字符处理（可能需要套路需要移除特殊字符么  特别国家的电话号码前面几位不一样这种

861   需要PM   目前是username字段超过25保存时候后端会提示字符长度不能超过25
859   ？（你需再要看看  我们前面看评论似乎是解决 但是看看评论时间  并没有被解决
846  待验证
828  我迷惑了 (注册逻辑没有districtId)
817  本地复现了 需要后端一起定位（目前看来完全不能修改权限 移除添加都不行）
802  frontend (目前是搜索结果中 Generate a temporary password 这个Button 点击后的模态框页面需要用到这个请求的数据)
========================================================================================================

748  ？  US dev处理 pending to close
738  backend
782/721/719/670  Collaborators先放一边
======================================

688 backend (需要后端放开all pages(not only first page)查询权限)
680 backend
TBOX-506 frontend (onboarding 后清除本地数据)
TBOX-175  frontend

## 问题

## 基础建设
- 基础组件的开发

## 质量保证
- 单元测试

## 优化
减少依赖 比如moment
添加mock功能 减少后端依赖 同步开发
错误处理
toast提示
错误边界都没有componentDidCatch


## announce
1. draft如何和其他状态转换以及如何编辑
2. pause 的功能逻辑
3. 编辑中的time  date name等字段不可编辑以及name是否必须？
4. 编辑中的 cancel 按钮的逻辑(包含draft)

============
- draft 下面编辑字段可以修改
- 添加一个bullet本地删除模态框  done
- 固定 submit header 栏
- 添加submit validate 



## branch 
1080 修复
1081 修复
1088 因为后端release time被重置
1079 1078  修复(同一个问题提了两遍)

======================
QA
1006

1006目前还可能存在的问题 
1. modal 关闭导致不能滚动
2. 创建时候的time 上下午 似乎没有区分
3. 切换tab是时间参数 没有获取到最新的
4. draft last-edit 是问题（后端没有更新）

其他 
active 转draft release time变为当前时间 没问题
schedule 转 draft release time改变（有问题
 

TODO
1. Toast组件添加submit tast
2. Modal问题

unit test
1. test date 和时区问题
2. mock 数据过时
3. 有效测试问题

Jest Runner vs插件可以方便的按文件测试





## latest
1. useScrollRequest
2. 实现webpack插件
3. 实现Toast组件

复习
1. react如何监听实践(componentDidMount)
2. react 中ref
  dom上是只dom节点， class Component 是指类组件实例  function component 没有ref  但是可以通过React.forwordRef包裹函数式组件来获取ref
3. addEventListener理解和好处
4. hooks理解和自定义Hooks运用
5. window.open记录日志
6. websocket https://medium.com/voodoo-engineering/websockets-on-production-with-node-js-bdc82d07bb9f

edituse modal 填充初始数据有问题
掌握useDispatch  useSelector useActions
做个class component 转 hooks插件？



need to merge branch
1 TBOX-1121-fix-bug   修复滚动的问题 以及what's new 时间相关的问题












