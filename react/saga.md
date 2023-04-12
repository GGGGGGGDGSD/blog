## 基本
Reducers 负责处理 action 的 state 更新

Sagas 负责协调那些复杂或异步的操作

1. takeEvery takeLatest 
  监听指定的action  然后执行新的effect 前者可以同时存在多个  后者只能同时存在一个  阻塞式
  
### Effect Creators 
  一个 Saga 所做的实际上是组合那些所有的 Effect，共同实现所需的控制流
1. call 调用effect 阻塞式
2. put 执行action 相当于dispatch 阻塞式
3. select 获取store中状态， 相当于store.getState()
4. fork 和call一样调用effect  但是是非阻塞式
5. take take函数可以理解为监听未来的action，



 SagaReturnType,
5. takeMaybe,
  all,


### saga 注册
const sagaMiddleware = createSagaMiddleware()
// 动态执行saga，注意：run函数只能在store创建好之后调用
sagaMiddleware.run(rootSaga)

## 相关资源
[参考](https://juejin.cn/post/6844903669305966599)
[Redux-saga 中文文档](https://chenyitian.gitbooks.io/redux-saga/content/)

### saga example
```ts
  export function* startNodeActionSaga({
  payload,
}: PayloadAction<NodeActionSubmitParams>): SagaIterator {
  const { agencyGuid }: Agency = yield select(agencySelector);
  const {
    historyData: { currentNodeId },
  } = yield select(reviewApplicationsSelector);
  const { toastText, nodeId, requestData } = payload;

  try {
    yield call(nodeActions, {
      agencyGuid,
      nodeId: nodeId || currentNodeId,
      requestData,
    });
    yield put(
      homeActions.showAlertMessage({
        type: 'success',
        content: toastText,
      }),
    );
    yield put(push({ pathname: RoutePathEnum.ReviewApplications }));
  } catch (error) {
    yield put(actions.submitWorkflowFormFailed());
  }
}

  export default function* paymentItemSaga(): SagaIterator<void> {
    yield takeLatest(actions.saveWorkflowForm.type, startNodeActionSaga);
  }
```
```js
// saga.test.js
it('should handle `reviewApplicationSaga` properly', () => {
    const iterator = reviewApplicationSaga();
    const step1 = iterator.next();
    expect(step1.value).toEqual(
      takeLatest(actions.fetchListData.type, fetchListDataSaga),
    );
    const step2 = iterator.next();
    expect(step2.value).toEqual(
      takeLatest(
        actions.fetchWorkflowDetailData.type,
        fetchWorkflowDetailDataSaga,
      ),
    );
    const step3 = iterator.next();
    expect(step3.value).toEqual(
      takeLatest(actions.submitWorkflowForm.type, startNodeActionSaga),
    );

    const step4 = iterator.next();
    expect(step4.value).toEqual(
      takeLatest(actions.startSaveForm.type, saveFormSaga),
    );

    const step5 = iterator.next();
    expect(step5.value).toEqual(
      takeLatest(actions.firstStepSubmit.type, firstStepSubmitSaga),
    );
    expect(iterator.next().value).toEqual(
      takeLatest(actions.createCustomer.type, createCustomerSaga),
    );
    expect(iterator.next().value).toEqual(
      takeLatest(actions.selectExistCustomer.type, selectExistCustomerSaga),
    );
    expect(iterator.next().value).toEqual(
      takeLatest(actions.searchCustomer.type, searchCustomerSaga),
    );
    expect(iterator.next().done).toBeTruthy();
  });
```