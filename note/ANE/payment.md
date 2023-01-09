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

 AUI: https://paymentmanagerui-vip.qa.aw.dev.activenetwork.com/login
 CUI: https://citizenui-vip.qa.aw.dev.activenetwork.com/DtestPMAgency?workflow=1

 CI:
 url: https://jenkins.aw.k8sw.dev.activenetwork.com/login?from=%2Fjob%2Fpayment-manager-ui-app-build%2F
 user/Password: fsun/+Active199204242515@



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
   