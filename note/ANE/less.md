


### 路由
- 通过createRouteCreator处理在module中routes目录处理

### style
- less
-  基础变量（需要熟悉
-  考虑响应式（媒体查询
-  命名规则  bem
- run style lint

### 响应式
- [具体操作文档](http://an-wiki.dev.activenetwork.com/development/tech-notes/front-end/responsive)
主要就是提供了判断判断啥平台的高阶组件withResponsiveProvider 以及以及针对mobile iPad pc三个比例的媒体查询

### 国际化
- react-intl
- [具体操作文档](http://an-wiki.dev.activenetwork.com/development/tech-notes/front-end/fe-multilingual-support)

### 目录结构
1 service
- api

2 redux
- consts
- actions
- reducer

3 style
- index.less

4 jsx
- index.jsx
- components

###  ui库
react-base-ui（需要熟悉

1. Message(提示/错误)
import { showError, clearError } from 'shared/utils/messages';



### 单元测试
1. view details of unit test by path test => coverage => index.html


### 日期处理
日期相关的公共方法： datetimeHelper.js
- 展示日期
```js
import { FormattedDate } from 'shared/translation/formatted';
<FormattedDate value={expiryDate} />
```


### 相关数据支持
- 自动化支持[data-qa-id](http://an-wiki.dev.activenetwork.com/development/tech-notes/front-end/automation-support)
  data-qa-id
  涉及输入或者操作的地方
  把相关数据提取到独立文件automationIds中

- 数据分析 [Tealium](http://an-wiki.dev.activenetwork.com/development/tech-notes/front-end/tealium)
这个目前可以不用关心



## code guide
### git

branch name
user-name/ticket-number

commit type

feat： 新增 feature
fix: 修复 bug
docs: 仅仅修改了文档，比如 README, CHANGELOG, CONTRIBUTE等等
style: 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑
refactor: 代码重构，没有加新功能或者修复 bug
perf: 优化相关，比如提升性能、体验
test: 测试用例，包括单元测试、集成测试等
chore: 改变构建流程、或者增加依赖库、工具等
revert: 回滚到上一个版本

### work flow 
1. 创建分支 Jira创建子任务 修改ticket状态 编码 合并develop分支代码 push到远程分支
 code => finshed test case => eslint styleEslint  eslint-fix 

2. 创建MR 处理test  case
- title: commit type: ticket number ticket describe
- assign to code reviewer
- watch jenkins and pipeline if success(import)
- handle MR comments
- write unit test and run pass success in local
- self-testing UAT case
- Log in work time
  
3. PO Meeting
- performance all test case by online site

4. update Jira and gitlab
- confirm the tag is generated
- add MR url to JIRA
- update subtask state to 'CLOSED'
  
Self-Testing here(http://an-wiki.dev.activenetwork.com/development/process/overall)


### immutable
- withMutations


### question
1. what's immediate sale membership and when trigger
2. Error display and Warning is related?


## Jest & Enzyme

1. action
   action & asyncAction

2. reducer

3. component
   shallow render
   - find
   - contains
   - equals
   - hasClass
   - is
   - exists
   - isEmpty
   - text
   - simulate
   - instance
  
  测试组件里面的方法 
  通过instance拿到组件实例调用方式

- [reference](https://enzymejs.github.io/enzyme/docs/api/shallow.html)



## WCAG
1. handle key event
```js
import { KeyCode } from 'react-base-ui/lib/consts';
import { listenKeyDown } from 'react-base-ui/lib/utils';

  onAddNewFamilyMemberKeydown = (e) => {
    e.stopPropagation();
    listenKeyDown(e, [KeyCode.ENTER, KeyCode.SPACE], () => {
      this.onAddNewFamilyMemberClick();
      e.preventDefault();
    });
  }
```

## QA
1. 啥时候使用context  configurations里面数据


### private lesson bookings
1. 尽早的进入调试阶段 这样才能尽早的发现问题
2. 尽早的提交， 这样才能可以尽早的code review  并且尽早的跑路pipeline是否通过

1. 入口通过mock account_configuration.json 文件控制
2. 路由不仅前端路由 还需要后端设置一个相同的路由重定向接口（否则切换语言时候会提示页面找不到
3. 面包屑和表单的文案后端提供
4. 票据表单渲染模版
//  myaccount/instructor 票据业务
> 后端提供渲染表单的json数据  然后前端通过ReportBaseForm组件渲染出表单 

## ticket
https://jirafnd.dev.activenetwork.com/browse/ANE-137541

## ReportBaseForm
###  参数
```js
<ReportForm
  reportId={reportId}  // 请求默认表单数据
  data={reportSearchFormGroup}  // 下拉选项数据
  formValueMap={formValueMap}   // form state value
  widgetUIStateMap={widgetUIStateMap}  // form ui control field
  setFormValueAction={setFormValueAction} // change form field value action
  setFormErrorAction={setFormErrorAction} // change form field error action
  setNoRecordAction={setNoRecordAction}
  setActivitiesAction={setActivitiesAction}
  isNoRecord={isNoRecord}
  errors={errors}  // form error value
  eventMap={eventMap}  // activity filter field handle
  formItemProps={formItemProps}
  validateEventMap={validateEventMap}
  data-qa-id={AMIds.reportBaseForm.warapper}
  ariaLabelMap={ariaLabelMap}
/>
```
#### 所有渲染基于下面这三步
1. utils => reportUtils封装了form相关的同步 异步action  reducer(form状态管理)
2. ReportBaseForm组件渲染表单具体字段（form 字段渲染管理）
3. component => reportBaseForm 获取渲染表单数据 以及activity数据 以及filter activity相关事件操作（form事件管理）

#### 应用form
```jsx
import { connect } from 'react-redux';
import { PRIVATE_LESSON_BOOKINGS_REPORT_ID } from '../../utils/reportUtils/consts/reportTypes';
import actions from '../actions';
import ReportBaseForm from '../../components/ReportBaseForm';

export default connect(
  state => ({
    reportID: PRIVATE_LESSON_BOOKINGS_REPORT_ID, //  后端提供固定的report ID
    reportFormState: state.modules.MyAccount.PrivateLessonBookings.privateLessonBookings  // 连接redux 里面的form状态
  }),
  {
    ...actions   // 提供覆盖操作form的action
  }
)(ReportBaseForm);
```

#### 渲染细节
1. 没有有效活动，空表单渲染
  ```js
  // 通过请求header数据判断  并提供渲染文案
  if (headers.response_code === ResponseCode.NO_RESULT) {
        dispatch(uiSetNoAvaibleActivities({ value: true }));
        dispatch(uiSetNoItemsMessage({ value: headers.response_mess
  ```

2. 星号相关处理逻辑
 字段级别完全有后端提供的required字段控制  sub_group sub title 的星号也是后端提供相同的字段控制
 在ReportForm文件中 
 - !isSm && pageHasRequierd && index === 0 && this.renderRequiredTips()} 渲染成 “*
is for required fields.”  判断逻辑是： 是否是第一个数组元素 其次整个表单中是否包含至少一个必选字段
- {subItem.get('required') && <span className="required-label">*</span>}  这部分渲染非第一个数组元素的sub

// mock data 
1. api file update mock path
2. test/json/ create mock data file





###business
#### Create Prospects Records

QA
1. 是否有相关和iframe通信
2. 进入页面之前是否需要预填充 是否需要用户数据
3. 提交后是否返回到哪 是否需要提供一个方法
4. 校验方法是否后端提供
5. 是否需要前端自己写一套渲染模版



### report
1. 2ticket 7 sp
2. 遇到一些问题
   - 多语言切换导致页面找不到问题（需要后端设置动态路由问题
   - configretion
3. 可优化
   1. 尽早的到自测阶段 尽早发现问题
   2. 业务理解不够透彻
   3. 自测不够完整













========================================================================================
## 三月总结

第一个月  熟悉工作流规范 搭建环境 跑test case熟悉业务  做的小demo
第二个月 比同期入职的晚一个月进入sprint  然后第一个sprint做了一个ticket两个点 第二个sprint做了7的点  这个sprint20个点

遇到一些问题
针对上面自己会刻意关注的点： 1. 确保完整的理解需求 2. 尽早的完成coding 然后有效的执行自测（1. 可能会改老功能 开关太多） 3 学会提问题以及找到正确的人

整体目标的话  让自己养成注重质量的习惯

========================================================================================





###
1. app.jsx 整个个应用入口
   AppRoot渲染（判断是服务器还是客户端
   initialize(各种资源初始化)
   ```js
    // initialize/index.js
    webfont.initialize(); // 字体
    theme.initialize(settings); // 主题
    gaService.initialize(config); // ？？
    tealiumService.initialize(store);  // ？？
    locationService.initialize(store); // ？？

    const { dateFormat, timeFormat } =
      getDateTimeFormatsById(config.date_format, config.time_format);
    const timeZoneOffset = isNaN(config.time_zone_offset_hour) ?
      undefined : parseInt(config.time_zone_offset_hour, 10);

    Globalize.ANDateFormat = dateFormat;
    Globalize.ANTimeFormat = timeFormat;
    Globalize.ANTimeZoneOffset = timeZoneOffset;
    responsive.setIsSupportResponsive(config.enable_cui_pc_responsive);

    requests.length && requests.forEach(requestInterceptor =>
      addRequestInterceptor(requestInterceptor));
    responses.length && responses.forEach(responseInterceptor =>
      addResponseInterceptor(responseInterceptor));
   ```
   
   redux store注入
   全局路由router注入

2. appRoot.jex 
   多语言国际化IntlProvider
   全局toast注册
   创建一个向下传递的context对象
   ```js
   getChildContext() {
    const { orgPath, configurations, systemSettings, responsive } = this.props;
    return {
      orgPath,
      configurations, // 应用配置
      systemSettings, // 应用相关设置参数
      responsive,   // 响应式
      theme: {      // 主题
        name: systemSettings.getIn(['customizeStyle', 'current_theme']),
        customizedColors: systemSettings.getIn(['customizeStyle', 'customized_theme'])
      },
      getWording: this.getWording.bind(this),   // ？？
      isLoginUser: this.isLoginUser.bind(this),  // 用户登陆状态
      getLogoutUrl: this.getLogoutUrl.bind(this)  // 用户登出URL
    };
  }
   ```
3. appRouter 跟路由注入（Router版本太老  没完全理解参数
4. 全局路由注入
   ```js
   // routes/index.js
   const globalRoutes = [  // 全局路由， 添加全新页面可以参考这个
      ...systemRoutes,
      ...unmatchedRoutes
    ];

    return (orgPath && orgPath !== '/' ? [
      ...receiptRouteCreator(),
      {
        ...orgRouteCreator(),
        childRoutes: [
          ...homeRouteCreator(),
          ...devAdminRouteCreator(),
          ...cartRouteCreator(),
          ...daycareRouteCreator(),
          ...
        ]
      },
      ...globalRoutes
    ] : globalRoutes);
   ```
5. orgRoute作为一级路由  对应master组件  这个组件做一些全局的事情 比如全局的header  footer 以及pageNotFound siteNotFound 全局的响应式设置  然后其他路由都是二级路由，也就是其他路由只控制content这部分
6. 页面布局layout.js文件有action控制 把页面分成了header navigation  content  footer四部分
7. 控制content内容。 包含layout(shared/components/Layout)  Breadcrumb MessageBoard  content  文件content/index.js，第一条提到的layout 文件控制页面布局的 action 的state  就是在这个页面引入shared/components/Layout 使用  主要是通过type来控制样式
```js
// content/index.js
 <Layout
    className="an-main__wrapper"
    type={this.props.layout.get('type')}
    style={this.props.layout.get('style')}
  >
    {
      !is404 ?
        (<PageHeader
          className={pageHeaderClass}
          routes={routes}
          showLogo={!isMobileOrTablet}
          headerText={specificHeaderFooter.get('header')}
        >
          {
            !isMobileOrTablet ?
              <Breadcrumb
                routes={routes.filter(route => route && route.path)}
                params={params}
              />
              : null
          }
        </PageHeader>) : null
    }
    <MessageBoard />
    {children}
  </Layout>
```
```js
//shared/components/Layout 
// state  layout: state.layout.get('content'),
import React from 'react';
import { node, string, oneOf } from 'prop-types';
import { FULLSCREEN, DEFAULT } from '../../consts/layout';
import './index.less';

export default class Layout extends React.PureComponent {
  static propTypes = {
    children: node,
    className: string,
    type: oneOf([FULLSCREEN, DEFAULT]),
    as: string
  }

  static defaultProps = {
    type: DEFAULT,
    as: 'div'
  };

  render() {
    const { type, children, className, as: As, style, ...rest } = this.props;
    return (
      <As
        {...rest}
        style={style && style.toJS()}
        className={`layout__container--${type === FULLSCREEN ? FULLSCREEN : DEFAULT} ${className}`}
      >
        {children}
      </As>);
  }
}
```

8. 触发控制页面布局的action（只讨论全屏
> 主要调用setFullScreenLayoutAction 这个action实现
```js
// appRouter.jsx componentDidMount  很明显这里设置全屏的配置  默认的页面宽度是960px
updateLayout(pathname) {
    // need show search bar in navigation
    const regexShowSearch = new RegExp(`(${SEARCH_BAR_PAGES.join('|')})$`, 'i');
    // need show fullscreen
    const fullScreenPages = [
      urls.HOME,
      urls.RESERVATION_HOME,
      urls.RESERVATION_LANDING_QUICK,
      urls.LEAGUE_INFO,
      urls.LEAGUE_TEAM_INFO,
      urls.LEAGUE_LIST,
      urls.YMCA_INTEGRATION
    ];
    const regexFullSceen = new RegExp(`(${fullScreenPages.join('|')})$`, 'i');

    const regexNewCart = new RegExp(`(${urls.NEW_CART})$`, 'i');
    if (regexFullSceen.test(pathname)) {
      this.props.setFullScreenLayoutAction(regexShowSearch.test(pathname));
    } else if (!regexNewCart.test(pathname)) {
      this.props.resetLayoutAction();
    }
  }
```

## 加载静态资源图片
1. 优先从后端获取  没有才再前端获取
```js
// window.__akamaiUrl point to local static resource image 
    const previewImg = hasImage && imageUrl ? imageUrl : `${window.__akamaiUrl}/images/campaign-default.png`;
```

## git token
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

## other
1. request
  使用 isomorphic-fetch 库
  import { HttpMethod, createAPI } from 'react-base-ui/lib/common/restClient';


## todo
1. react18
2. 函数式编程



## YMCA
1. banner 图片长宽比例是否固定 图片是否区分移动端
2. 切换语言是否会像Cui其他页面一样会刷新页面并从服务器拉去数据（这个似乎是前端的活

PO meeting
1. dropdown please select选项 移除
2. dropdown 默认显示Operator
3.  cell phone number 添加 “*”
4.  dropdown的选项不能换行




## Instructor  mobile 入口配置
file: /Users/ysong/project/cui/src/index/modules/MyAccount/AccountOptions/components/Instructor/index.jsx
开关: /Users/ysong/project/cui/src/index/modules/MyAccount/AccountOptions/consts/groupOptionNames.js

## 查看构建版本
路由：rest/version

## AAUIDropdown组件
1. devtool 调试 保持展开  可以通过添加show class控制
1. 不换行
   ```css
   .dropdown__menu {
      width: auto;
    }
    .option-content__text {
      white-space: nowrap;
    }
   ```


## PersonalInformation. 组件位置


path: /Users/ysong/project/cui/src/index/modules/MyAccount/PersonalInformation


email. Reg   path:
/Users/ysong/project/react-base-ui/src/services/validation/rules/email.js

Action path:

/Users/ysong/project/cui/src/index/modules/MyAccount/PersonalInformation/actions/contactInformation.js


Shard:
/Users/ysong/project/cui/src/shared/rules/formRules.js


## ANE-138866
1. 问题
  1. 应该今天的先去测试这个参数  这样才能尽早的暴露后端是否有问题  方便其尽早修复
  2. 解决问题方式确实有点问题  最主要还是没有完全里面整个ticket的逻辑  交互逻辑 比如email还是一对字符串  这样一开始就能定位到在字符串里面处理img标签
  3. 正则和交互状态浪费了太多时间
  4. 单元测试还不够熟悉  特别是涉及组件和异步action

2. 用到技术点
  1. 工具函数能用lodash就用  join  map uni isFunction
  2. 清除子组件内部状态： 传递一个toggle 在componentWillRecieveProps监听toggle的变化
  3. 下载报表请求用这个 import { ReportDownloader } from 'shared/services';
  4. 各种message使用
    ```js
      // 1. page message
      import { showSuccess, clearSuccess, showError, clearError } from 'shared/utils/messages';

      // line error
      import ErrorItem from 'shared/components/ErrorItem';

      // modal error
      import Alert2 from 'react-base-ui/lib/components/Alert/Alert2';
     
     // Toast
     import * as Toasts from 'shared/utils/toasts';
    Toasts.showOnce({ content: messages[selfMessages.sendSampleEmailNotify.id] }, { position: 'center' });

    // Validation scroll to first error
    scrollToFirstError = () => {
      const { responsive: { isLg } } = this.props;
      setTimeout(() => {
        const errorItemClassNames = [
          'email-participants__subject-error',
          'email-participants__send-sample-email-modal-error',
          'message-board .alert-error',
          'membership-enroll-form__missing-prerequisite',
          'primary-holder-error',
          'input-group-error',
          'enrollment-detail-renewal-error',
          'question-answer__error',
          'shared-donation__error'
        ];
        const errorItem = errorItemClassNames.reduce((acc, cur) => {
          if (!acc) {
            acc = document.querySelector(`.${cur}`);
          }
          return acc;
        }, null);

        if (errorItem) {
          const mobileSticky = document.querySelector('.an-sticky');
          const offset = mobileSticky ? mobileSticky.offsetHeight : 0;
          const scrollDistance = isLg ? errorItem.offsetTop :
          errorItem.offsetTop - offset;
          window.scrollTo({
            top: scrollDistance,
            behavior: 'smooth'
          });
        }
      }, 30);
    }
    ```
    
  5. 各种替换正则
    ```js
    // 替换html实体符号
    export const escape2Html = (str) => {
      const arrEntities = {
        lt: '<',
        gt: '>',
        nbsp: ' ',
        amp: '&',
        quot: '"'
      };

      const reg = new RegExp(/&(lt|gt|nbsp|amp|quot);/, 'ig');

      return str.replace(reg, (all, t) => arrEntities[t]);
    };

    // 正则表达式放入变量
    // new RegExp支持放入变量
     const regText = `%%${replaceSpecialCharacterText}%%`;
     const reg = new RegExp(regText, 'g');

     // replace使用
      import { escape2Html } from '../utils/escape2Html';

      export const getReplaceImgAttrOrder = (str) => {
        const getImageSrcReg = /src(\S)+\s/;

        const replaceFn = (match, p1, p2, p3, p4) => {
          const [srcString] = p2.match(getImageSrcReg) || [];

          return escape2Html(`${p1} ${srcString + p2.replace(/src(\S)+\s/, '')}${p4}`);
        };

        //  通过（）设置不过组  这样方便后面拿到跑p1. p2. p3. p4  还有非贪婪模式
        // 最后还要注意前向断言和后向断言不要用 iOS不支持
        const getImgStringReg = new RegExp(/(<img)((.)+?)(>)/, 'g');
        return str.replace(getImgStringReg, replaceFn);
      };
    ```

    6. 页面权限访问
   
      ```js
      // 如果开关是关闭的 就让页面返回page not found
      const isEnableEmailparticipants = configurations.get(
          'redesign_on_cui_my_account_email_participant'
        );

        if (!isEnableEmailparticipants) return {};
      ```




```js
//   最核心参数
return {
    EmailSubject: formValue.get('subject'),
    Activity66: join(uniq(map(formValue.get('activities'), 'id')), ','),

    EmailBodyType: '1', //  默认“1” //   recipients? attachments
    EmailCCAddress: formValue.get('cc'),
    xnetframe: false,
    rptno: '586', // 给不给都行
    EnrollType: '2',  // recipients type
    sdireqauth: '',  // 待确认？
    FieldInsert: '%%CustomerTitle%%', // 可以不用传
    rte1: 'asdasdasdsaddasdasdas', //  和 EmailBodyText
    // emailaddressfrom: user.get('email'),  // 先试试不传
    emailaddressfrom: 'yi.song@activenetwork.com',  // 先试试不传
    UploadedFile91: join(formValue.get('attachments'), ','),  // 附件
    // instructor_id: user.get('customerid'), // 先试试穿空
    instructor_id: '', // 先试试穿
    // EmailBodyText: 'asdasdasdsaddasdasdas',
    emailnamefrom: 'Mr. Charlie Wang', // 后面看看能否拿到
    OptOutSubscriptionList: emailAdvancedSettings.getIn(['OptOutSubscriptionList', 'value']),
    RetiredCustomerFilter: emailAdvancedSettings.getIn(['RetiredCustomerFilter', 'value']),
    CustomerNameFormat: emailAdvancedSettings.getIn(['CustomerNameFormat', 'value']),
    EmailsAndLabels: emailAdvancedSettings.getIn(['EmailsAndLabels', 'value']),
    uniqueemails: getMailConfigurationData(emailAdvancedSettings, 'uniqueemails'),
    IncludeAdditionalEmailAddress: getMailConfigurationData(emailAdvancedSettings, 'IncludeAdditionalEmailAddress'),
    IncludeNoMailCustomers: getMailConfigurationData(emailAdvancedSettings, 'IncludeNoMailCustomers'),
    IncludeNoPostalMailCustomers: getMailConfigurationData(emailAdvancedSettings, 'IncludeNoPostalMailCustomers'),
    sortid: emailAdvancedSettings.getIn(['sortid', 'value']),
    DefaultAddress: emailAdvancedSettings.getIn(['DefaultAddress', 'value']),
    SampleEmailAddress: join(uniq(map(submitSection.get('sendSampleEmail').toJS(), 'email')), ',')
  };
```

## ANE-142722
```js
 path: 'daycare/program/enroll/:programId',
    indexRoute: {
      component: Daycare.EnrollForm,
      if (
              reservationUnit === RU.DAILY ||
              reservationUnit === RU.WEEKLY ||
              reservationUnit === RU.MONTHLY
            ) {
              nextState.routes[2].component = Daycare.EnhancedEnrollForm;
            }
```
responsive MR: https://gitlab.dev.activenetwork.com/ActiveNet/cui/-/commit/eb81c1c7ac7a3238c9ccd80ed1dbf57413fd526a
 User Story 4.4: Responsive - Form Page - No Choice - All except Enrollment details section: https://jirafnd.dev.activenetwork.com/browse/ANE-84475

1. 读屏规则
   http://ux.active.com/wireframes/ANE/WCAG%20Guideline%202.0/#p=calendar&id=58gb00&g=1


## ANE-142723


============
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


## ANE-143383
>  关于这ticket 难以置信  input上面除了有 onpaste事件 还能得到 selectionStart， selectionEnd 等属性
 const { selectionStart, selectionEnd, value: previousValue } = event.target;


## 关于request
1. API => createAPI => Request =>  isomorphic-fetch
  path: /Users/ysong/project/react-base-ui/src/common/restClient/createAPI.js
  response 是被处理过的

  ```js
    // 只有code为 ’0000‘ 或者 ’0001‘ 两种判断为成功 其他都判为失败 走Promise.reject(在catch中捕获)
    const parseResponse = (jsonResponse, path, showLoadingBar) => {
    const response = new Response(jsonResponse);

    showLoadingBar && pageLoading.hide();

    if (response.success) {
      return Promise.resolve(response);
    }

    const titleOfServiceError = Globalize.translate(errorMiddleWare.serviceError.id);
    const msgGroup = new Message(MessageType.ERROR, response.message, titleOfServiceError);
      return Promise.reject(new ErrorObj(ErrorType.SERVICE, msgGroup, {
        code: response.code,
        url: path,
        response
      }));
    };
  ```
  ```js
  //Response
  const SuccessCodes = pick(ResponseCode, ['SUCCESS', 'NO_RESULT']);

  export default class Response {
    static isSuccess(responseCode) {
      const code = find(SuccessCodes, value => value === responseCode);
      return !!code;
    }
  ```


  

关于response code
/Users/ysong/project/react-base-ui/src/common/restClient/consts/ResponseCode.js

peer sprint output bug
134 2
135 7
136 10
137 16
138 10
139 15
140 17 + 3
141 17
142 8
143 5