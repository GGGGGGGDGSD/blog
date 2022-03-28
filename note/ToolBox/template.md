## Toast
=========================================================
```js
// constants
  TOAST_DISTRICT_LOOKUP                      : 'districtLookup',
  TOAST_DISTRICT_LOOKUP_FAILURE_TYPE         : 'districtLookupFailure',

// actionCreator
const toastText = 'success!';
dispatch(ToastActions.updateToastInfo({
  id      : ToastConstants.TOAST_DISTRICT_LOOKUP,
  options : {
    toastType: ToastConstants.TOAST_DISTRICT_LOOKUP_FAILURE_TYPE,
    toastText,
  },
}));
setTimeout(() => {
  dispatch(ToastActions.resetToast(
    ToastConstants.TOAST_DISTRICT_LOOKUP_FAILURE_TYPE,
    ToastConstants.TOAST_DISTRICT_LOOKUP,
  ));
}, ToastConstants.TOAST_TIMEOUT_DURATION);

// view
import ToastNotification from '../../../users/common/ToastNotification';
import ToastConstants from '../../../../constants/ToastConstants';
import { selectSpecificToastInfo } from '../../../../selectors/ToastSelectors';
import ToastHelper from '../../../../model_helpers/ToastHelper';

// mapStateToPorps
toastInfo             : selectSpecificToastInfo(state, ToastConstants.TOAST_DISTRICT_LOOKUP),

// render
const toastText   = ToastHelper.getToastText(toastInfo);
const toastType   = ToastHelper.getToastType(toastInfo);
<ToastNotification toastText={toastText} isOpen={!!toastText} toastType={toastType} />
```







## loading
===============================================================
```js
// constants
  BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL             : 'BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL',
  BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL_COMPLETED   : 'BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL_COMPLETED',

// actionCreator
dispatch(beginAjaxCallAction(
  AjaxCallStatusConstants.BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL,
  StoreStateConstants.VIEW_ALL_ANNOUNCEMENT_FETCH_STATUS,
));

dispatch(beginAjaxCallAction(
  AjaxCallStatusConstants.BEGIN_NEW_FEATURE_ANNOUNCEMENT_FETCH_AJAX_CALL_COMPLETED,
  StoreStateConstants.VIEW_ALL_ANNOUNCEMENT_FETCH_STATUS,
));

// view
function mapStateToProps(state, ownProps) {
  return {
    activeAnnouncementsStatus    : selectSpecificStatus(state, StoreStateConstants.VIEW_ALL_ANNOUNCEMENT_FETCH_STATUS),
  };
}
```


## tooltip
=================================================================
```js
  const [tooltipOpen, setTooltipOpen] = useState(false);
  const toggleTooltip = () => { setTooltipOpen(!tooltipOpen); };


<i id="Audience" className="fas fa-exclamation-circle cursor-pointer" />
 <Tooltip placement="top" isOpen={tooltipOpen} target="Audience" toggle={toggleTooltip}>
  {
    `
    A/T/S/P = 
    Administrator/Teacher/Student/Parent
    `
  }
  </Tooltip>
```



## 分页
==============================================================
1. view
  
```js
import { useLocation } from 'react-router-dom';
import queryString from 'query-string';
const location = useLocation();
  const [page, setPage]                   = useState(1);
    useEffect(() => {
    const { page: currPage = 1 } = queryString.parse(location.search) || {};

    if (Number(currPage) !== page) {
      setPage(Number(currPage));
    }
  }, [location]);


 <PaginationNav totalPages={totalPages} currentPage={page} path={location.pathname} />


 function mapStateToProps(state, ownProps) {
   // 这里有细节 意味着ownProps要传进去page参数  那意味着page只能是在父组件传入
  return {
    totalPages   : selectTotalPages(state, ownProps),
  };
}
```

## class 样式名覆盖
由于ruby webpack 打包顺序有问题 可采用这种命名空间加样式名方式增加优先级
```css
.CountryBulkActionTab {
  .bulk-btn-selected {
    color: #fff;
    background-color: #2971bb;
    border-color: #276bb0;
    box-shadow: 0 0 0 0.2rem rgba(85, 150, 218, 50%);
  }
}
```

## 
bootstrap_overrides 引入bootstrap样式


### 添加新的路由页面
1. App.js页面注册路由
2. LeftColumn 添加侧边栏选项
3. 上面两个页面用到各种常量
4. routes.rb 页面配置路由权限

### bulk upload flow 
 1. bulkUpload 文件  返回一个jobId
 2. startPolling 通过jobId监听文件上传进度
 3. runPolling 通过不断的重试来监听数据（三种状态 成功 失败  超时）
 4. onPolling 监听的数据（ running_status replication_lags filename, sync_job_status(通过这个来判断是否需要重试)
 5. onSuccess 成功后调用 uploadCompleteAction fetchCurrentJobProgressSuccessAction
  
/*
  bulk upload            request
  districts
  regions
  schools
  teachers
  students
  groups
  district_admins
  school_admins
  groups              classes
                  enterprise_admins
  memberships
*/
