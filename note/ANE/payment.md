## env
- node   版本  v16.16.0
yarn 版本 1.22.17

yarn config set registry https://artifacts.dev.activenetwork.com/artifactory/api/npm/npmjs

sudo -- sh -c -e "echo '127.0.0.1   localhost.dev.activenetwork.com' >> /etc/hosts" 

每次启动yarn start之前需要在postman调用token接口拿到token替换到frontend/src/shared/lib/session.ts文件的jwtToken字段

## 技术栈
chakra-ui + saga + styled + ts

## 账号 (需要连接公司网络)
user： demi.zhang@activenetwork.com
password: Pos@test

nancy_superadmin@test.com
密码：PWDpm123!

jasmineAgencyPinPadOpened
JasmineAgencyPinPadClose


 AUI: https://paymentmanagerui-vip.qa.aw.dev.activenetwork.com/login
 CUI: https://citizenui-vip.qa.aw.dev.activenetwork.com/DtestPMAgency?workflow=1

 CI:
 url: https://jenkins.aw.k8sw.dev.activenetwork.com/login?from=%2Fjob%2Fpayment-manager-ui-app-build%2F
 user/Password: fsun/+Active199204242515@

 ## JF 账号
 https://college-web-q-jf.dev.activenetwork.com/
 democompliance@activenetwork.com
 @ctive123



## front-desk
- 这个主要基于react-flow-renderer(现在叫react-flow 我们使用时老版本)库来开发
- [react-flow](https://reactflow.dev/docs/guides/custom-nodes/)

Flow文件夹定义基本的节点： customerNode conditionEdge customerEdge endNode

### 页面部分：主要两个页面（list页面和detail chart页面）以及modal部分
  ```js
  // 页面类型。可以在react dev tool components中查看到常见组件对应的视图
  export enum WorkflowBuilderViews {
    ListView = 1,
    DesignerView = 2,
  }

  // modal类型
  export const MODAL_COMPONENTS: ModalTypesType = {
  CREATE_WF: CreateWorkflowModal,
  CONFIRM_WF: ConfirmModal,
  CONFIRM_WF_PUBLISH: ConfirmModal,
  EDIT_STEP_NODE: CreateStepModal,
  EDIT_START_NODE: EditStartModal,
};
  ```
- 节点类型
  ```js
   <!-- 这个文件能看到大部分的基本数据：frontend/src/constants/enumerations.ts -->
    export enum FlowNodeType {
      Start = 1,
      End = 2,
      Step = 3,
      Condition = 4,
      Action = 5,
    }
  ```

  ## Jira
  1. PL-310 关于Assignee单选问题 需要从外面传递一个参数isMulti 到createStep文件来控制Reselect组件为多选
   在文件front-desk/src/modules/payment-configuration/scenes/Workflow.tsx 添加如下
   ```jsx
   const onGetApplicationContentFields = useCallback(
    (keys: string[], callback) => {
      callback(
        keys.map((key) => {
          console.log('=========== ~ Workflow ~ keys: %d', keys);

          if (key === 'forms') {
            return { key, values: formatCustomForms };
          }
          if (key === 'NODE_FIELD_ACTION_TYPE') {
            return { key, values: StepType };
          }
          // 主要添加这部分
          if (key === 'NODE_FIELD_ASSIGNEE') {
            return {
              key,
              values: [...stepAssigneeList, ...formatUserList],
              isMulti: true,
            };
          }
          return {
            key,
            values: null,
          };
        }),
      );
    },
    [formatCustomForms, formatUserList],
  );
   ```
   但是下面仍然拿不到数据 需要根据如下开下开关
   ```jsx
   // path: frontend/src/containers/index.tsx
   const filterAttributes = (n: Types.IWorkflowNodeAttributeExtension) =>
      !n.isPermissions &&
      n.controlType &&
      n.controlType === FormControlTypes.Select &&
      n.visible;
   ```
   其次 取数据位置添加我们传递的数据
   ```jsx
     // path: frontend/src/containers/Slices/flowBuilderSlice.ts
     state.applicationContext.workflowConfig?.stepAttributes?.forEach(
        (s) => {
          if (s.name === k.key) {
            s.options = k.values;
            // 添加以下
            s.isMulti = k.isMulti;
          }
        },
      );
   ```

   ### Responsive
   1. js: react-responsive
   
   ```jsx
      export const DESKTOP = '1024';
      export const TABLET = '768';
      export const MOBILE = '360';

      import { useMediaQuery } from 'react-responsive';

      const isDesktop = useMediaQuery({
        query: 'only screen and (min-width: 1024px)',
      });
      const isMobile = useMediaQuery({
        query: 'only screen and (min-width: 360px) and (max-width: 767px)',
      });
      const isTablet = useMediaQuery({
        query: 'only screen and (min-width: 768px)',
      });
   ```
   
   
   ## PL-458
   2. from version text
   3. current step 文案变更
   4. 没有下边的按钮
   5. assignee-avatar
   6. mobiles steps 里面的close icon是否固定
   <!-- 6. 滚动穿透问题 -->
   7. 返回的icon


## today
误用了git stash drop
git fsck –lost-found(https://blog.csdn.net/weixin_44388689/article/details/120076830)

1. npm link 本地多项目调试
   npm link invalid hook call

2. CUI workflow list 页面  
  ?workflow=1

3 作ticket之前一定要调研清楚
1. 清楚ticket本身业务逻辑
2. 清楚


问题记录：
1. 刷新页面 下面多了一块出来 - 苹果
2. action button上面的margin问题  （有一块较宽的空白）（tablet content bottom padding)            Done
3. 三星手机展开键问题（有一个蓝色条条）（所有的可点击地方都有这个问题  
4. Not started的位置问题 (tablet mobile history bar)     Q
5. 只有步骤和not started  展开收缩问题(tablet mobile history bar)  Q
6. workflow名字过长 ipad上人的名字显示位置问题  人的名字太长workflow显示问题  Done
7. hirstory bar里的内容 往上滑 下面的内容显示在了x那一栏的上方               Done
8. ipad上header被截断如果往上滑 滑动form不太流畅 (content margin top tablet)
9. 唤起键盘页面滚动UI有问题(mobile) 外层滚动
10. 三星手机  名字太长 没有换行                                           Done
11. 三星平板 如果光标定位在第一个问题 唤起了键盘 最后一个问题滚动不出来        待验证
12. 姓名太长 第一个history bar card, expand collapse与实际的行为不一致 （展开收缩逻辑怪异  Q


## question
1. 现在最主要问题是如何本地调试设备 域名不支持访问
2. 缺少一些公共responsive处理
   1. mobile蓝色块
  -webkit-tap-highlight-color: transparent;

  const { close } = ConfirmModal.confirm({
      title: i18n('application.detail.deny.label'),
      content: <ModalContentWrapper ref={commentRef} />,
      onOk: async () => {
        const { verified, save } = formRef.current;
        const textareaElement: HTMLFormElement = commentRef.current;
        if (!verified()) return;

        const formData = await save();
        dispatch(
          actions.submitWorkflowForm({
            agencyGuid,
            nodeId: parseInt(nodeGuid, 10),
            toastText: i18n('application.detail.toast.denied'),
            requestData: {
              actionType: 'DENY',
              comment: textareaElement.value,
              formData,
            },
          }),
        );
      },
      okText: i18n('application.detail.btn.deny'),
      cancelText: i18n('application.detail.btn.cancel'),
    });
    modalInstanceCloser = close;

## Charles代理配置
chls => help => ssl proxying => remote mobile notice
1. 手机端设置手动代理  代理iP和端口
2. 访问chls.pro/ssl 下载CA证书
3. 在WALN高级安装证书
4. 设置信任证书
5. 访问

CUI QA 
https://citizenui-vip.qa.aw.dev.activenetwork.com/PaymentManagerACH?workflow=true
https://citizenui-vip.qa.aw.dev.activenetwork.com/PaymentManagerACH/workflow/11460


https://localhost.dev.activenetwork.com:3000/jasmineAgencyPinPadOpened44

CUI-int
https://citizenui-vip.int.aw.dev.activenetwork.com/jasmineAgencyPinPadOpened?workflow=1
  

在PM调试好让后把代码等量落到form inbox

env(safe-area-inset-left)

@media only screen and (orientation: landscape) {
    body {
        background-color: lightblue;
    }
}

防御性css
https://article.itxueyuan.com/GjlqAZ

HistoryType Detail firstName lastName

// TODO
/*
1. only view 以及展示reject 内部逻辑有点问题
2. 重新加载
3. textarea


1. 只有1 step  assign 给自己  CUI提交AUI为啥收不到

*/


ConfirmModal


##  禁用ts lint
ForkTsCheckerWebpackPlugin


## Sprint43 ISD Retro Meeting Notes
Hi all,
 
Please see the attachment.
And try to avoid the same issues.
 
Some good practice actions for you.
 
Read AC carefully.
Raise risk as early as you can if you find something is not in controll.
Take more Self Testing. Complete the code as early as you can.
Commit your code to review as early as you can. So that othere members have enough time to read and test your code.
PO review is necessary. It could help you avoid some bugs.
Ask other members to help you do test.
 
And here is the retro git address.
 
https://gitlab.dev.activenetwork.com/activeworks-platform-shared-projects/payment-manager/docs/-/blob/master/development/scrum/isd_retro_notes.md
 
Enwei