## rbac前端设计与记录
 ### 实现效果
 - 不同的用户看到不同的菜单以及不同的Button操作权限
 - 页面之间跳转到没权限访问的路由友好显示为 not exist页面
 - 手动在地址栏输入没权限访问的路由友好显示为 not exist页面
 
 ### 核心思路
  **1. 数据结构**
  
  从前端的角度，加载应用后首先展示的就是菜单，然后在通过菜单导航到具体页面，这意味着需要获得一个菜单级别（路由级别）的权限表，其次是页面级别的权限表以及一个角色表
  
  - 菜单级别权限表决定菜单如何展示，以及路由渲染
  - 页面级别权限表决定页面具体的按钮是否展示 可操作等
  - 角色表目前很少。如果能拿到当前用户的具体操作权限，至于是什么角色其实我们可以不用关心，正是基于此，没怎么使用角色，后面可能会考虑辅助控制具体页面级别的bottom
  
  **2. 关联**
  
  - 需要控制Route路由渲染, 菜单渲染，拿到具体路由的权限，能关联这些只有路由地址，所以路由会成为后面关联各种操作的核心节点
  - 需要保证路由地址的唯一性。我们目前应用的菜单基本都是二级菜单，所有我们把一级路由+二级路由 作为一个操作权限模块（保证唯一性）
  - 三级路由通过地址拿到二级路由的具体操作权限操作

### 实现前一些思考

   - 如何知道哪些菜单是展示 哪些隐藏
   - 如何知道当前菜单有哪些具体的权限
   - 如何把Route LeftColumn（menu）渲染和rbacKey关联起来

 ### 实现
   **1. 计算菜单级别的权限表**
   > 配置rbac路由映射表routeRbacMap, 配置规则：通过[这个表](https://shimo.im/sheets/5s64xm0zkT4vCuKy/ZruKR)计算对应rbacKey对应的路由(目前只考虑到二级路由)
   ```js
    // key = rbacKey  value = url
    const RbacRouteMap = {
     'superuser_tools#delete_superuser'                           : 'superusers/list',
     'superuser_tools#superusers'                                 : 'superusers/list',
     'superuser_tools#takeover_history'                           : 'superusers/list',
     'superuser_tools#update_superuser'                           : 'superusers/list',
     'customer_support_vendors#create'                            : 'superusers/customer_support_vendors',
     'customer_support_vendors#index'                             : 'superusers/customer_support_vendors',
     'customer_support_vendors#update'                            : 'superusers/customer_support_vendors',
     'institution_admin_rights#destroy'                           : 'admin_tools/institution_admin_rights',
     'institution_admin_rights#index'                             : 'admin_tools/institution_admin_rights',
   }
  ```
 
 **2. 路由级别的权限表结构。最终放进状态管理的是下面第二种结构，因为这种结构更方便后面使用**
 - 扁平的key-value结构
 ```javascript
   const rbacKeyValueMap = {
     bulk_admin_rights#bulk_grant: undefined,
     bulk_rosterings#process_district_admins: undefined,
     bulk_rosterings#process_districts: undefined,
     bulk_rosterings#process_groups: undefined,
     bulk_rosterings#process_memberships: undefined,
     bulk_rosterings#process_regions: undefined,
     bulk_rosterings#process_removal_members: undefined,
     bulk_rosterings#process_school_admins: undefined,
     bulk_rosterings#process_schools: undefined,
     bulk_rosterings#process_students: undefined,
     bulk_rosterings#process_teachers: undefined,
     customer_support_vendors#create: "superusers/customer_support_vendors",
     customer_support_vendors#index: "superusers/customer_support_vendors",
     customer_support_vendors#update: "superusers/customer_support_vendors",
     districts#create: "institutions/index",
     enterprise_account_licenses#update: "enterprise/country_accounts",
     enterprise_account_settings#clear_sub_institution_settings: "enterprise/country_accounts",
     enterprise_account_settings#create: "enterprise/country_accounts",
     enterprise_account_settings#destroy: "enterprise/country_accounts",
     enterprise_account_settings#index: "enterprise/country_accounts"
     enterprise_account_settings#supported_setting_types: "enterprise/country_accounts",
     enterprise_accounts#assign_admin_rights: "enterprise/country_accounts",
     enterprise_accounts#basic_stats: "enterprise/country_accounts",
     enterprise_accounts#bulk_create_districts: "enterprise/country_accounts",
     enterprise_accounts#destroy: "enterprise/country_accounts",
     enterprise_accounts#district_admins: "enterprise/country_accounts",
     enterprise_accounts#enterprise_admins: "enterprise/country_accounts",
     enterprise_accounts#index: "enterprise/country_accounts",
     enterprise_accounts#invite_members: "enterprise/country_accounts",
     enterprise_accounts#remove_admin_rights: "enterprise/country_accounts",
     enterprise_accounts#school_admins: "enterprise/country_accounts",
     enterprise_accounts#update: "enterprise/country_accounts",
     enterprise_conflict_emails#bulk_send_activation_emails: "enterprise/country_accounts",
     enterprise_conflict_emails#convert_users: "enterprise/country_accounts",
     enterprise_conflict_emails#index: "enterprise/country_accounts",
     institution_admin_rights#destroy: "admin_tools/institution_admin_rights",
     institution_admin_rights#index: "admin_tools/institution_admin_rights",
     metadata#countries: "users/search",
     schools#create: "institutions/index",
     superuser_tools#delete_superuser: "superusers/list",
     superuser_tools#superusers: "superusers/list",
     superuser_tools#takeover_history: "superusers/list",
     superuser_tools#update_superuser: "superusers/list",
     sync_accounts#destroy: "enterprise/country_accounts",
     sync_job_items#index: "enterprise/country_accounts",
     sync_jobs#bulk_onboarding_steps: "enterprise/country_accounts",
     sync_jobs#configuration: "enterprise/country_accounts",
     sync_jobs#configure: "enterprise/country_accounts",
     sync_jobs#create: "enterprise/country_accounts",
     sync_jobs#index: "enterprise/country_accounts",
     sync_jobs#records_created_stats: "enterprise/country_accounts",
     sync_jobs#stats: "enterprise/country_accounts",
     sync_jobs#status: "enterprise/country_accounts",
     sync_jobs#update: "enterprise/country_accounts",
   }
   ```

 - 有层级的映射表
  // 1. 最外层的key代表第一级路由
  // 2. children 代表子菜单
  // 3. children里面的key代表第二级路由
 ```javascript
   const authMap = {
     users: {
       name     : 'users',
       url      : '/users/',
       children : [
         { '/users/search': ['api1', 'api2', 'api3'] },
         { falgged: ['api1', 'api2'] },
       ],
     },
     enterpriseAccounts: {
       name     : 'enterprise Accounts',
       url      : '/enterprise/country_accounts',
       children : [
         { countryAccounts: ['api1', 'api2'] }
       ],
     },
   };
 ```

**3. 路由渲染权限控制**
  > 通过高阶组件ProtectedRoute来渲染可访问的路由
  具体逻辑：通过Route组件传递进来的参数pathname计算得到第一级路由和第二级路由，通过这两个参数以及权限表可判断当前路由是否可访问
  ```js
  import React from 'react';
  import { Route } from 'react-router-dom';
  import NotFound from '../404_page/404Page';

  const ProtectedRoute = ({
    currentUserRouteRbac,
    path,
    currentUser,
    ...rest
  }) => {
    const isLogin = currentUser && currentUser?.get('name');
    const [firstLevelMenu, secondLevelMenu] = path?.slice(1)?.split('/');

    if (!isLogin) return null;

    const hasAccessRbacInfo = currentUserRouteRbac && currentUserRouteRbac[firstLevelMenu]?.children[secondLevelMenu];

    if (hasAccessRbacInfo && hasAccessRbacInfo.length) {
      return <Route exact path={path} {...rest} />;
    }

    if (currentUserRouteRbac && !(hasAccessRbacInfo && hasAccessRbacInfo.length)) {
      return <Route path="*" component={NotFound} />;
    }
    return null;
  };

  export default ProtectedRoute;
  ```

**4. 菜单渲染**
> 核心逻辑和上面一样
```js
// menuList.js
import PagePathConstants from '../../../constants/PagePathConstants';
import LeftColumnConstants from '../../../constants/LeftColumnConstants';
import InstitutionConstants from '../../../constants/InstitutionConstants';
import StoreStateConstants from '../../../constants/StoreStateConstants';

const menuList = [
  {
    name     : LeftColumnConstants.SUPERUSER_TOOLS,
    value    : LeftColumnConstants.SUPERUSERS,
    pathname : 'superusers',
    children : [
      { name: LeftColumnConstants.SUPERUSERS, pathname: PagePathConstants.SUPERUSERS_PAGE_PATH },
      { name: LeftColumnConstants.LDAP_MAPPING, pathname: PagePathConstants.LDAP_MAPPING, search: '?page=1' },
      { name: LeftColumnConstants.CUSTOMER_SUPPORT_VENDORS, pathname: PagePathConstants.CUSTOMER_SUPPORT_VENDORS },
    ],
  },
  {
    name     : LeftColumnConstants.USERS,
    value    : LeftColumnConstants.USERS,
    pathname : 'users',
    children : [
      { name: LeftColumnConstants.SEARCH, pathname: PagePathConstants.USER_SEARCH_PATH },
      { name: LeftColumnConstants.FLAGGED, pathname: PagePathConstants.USER_FLAGGED_PATH, search: '?page=1' },
      { name: LeftColumnConstants.TAKEOVERS, pathname: PagePathConstants.USER_TAKEOVERS_PATH, search: '?page=1' },
      { name: LeftColumnConstants.BADGES, pathname: PagePathConstants.USER_BADGES_PATH },
      { name: LeftColumnConstants.CHAT_SEARCH, pathname: PagePathConstants.CHAT_SEARCH_PATH },
      { name: LeftColumnConstants.POSTS, pathname: PagePathConstants.POST_SEARCH_PATH },
      { name: LeftColumnConstants.NINJAPASSWORDS, pathname: PagePathConstants.USER_NINJAPASSWORDS_PATH },
      { name: LeftColumnConstants.EGYPT_STUDENTS, pathname: PagePathConstants.USER_EGYPT_STUDENTS_PATH },

    ],
  },
  {
    name     : LeftColumnConstants.INSTITUTIONS,
    value    : LeftColumnConstants.INSTITUTIONS,
    pathname : 'institutions',
    children : [
      { name: LeftColumnConstants.SEARCH, pathname: PagePathConstants.INSTITUTION_SEARCH_PATH, search: `?filter=${InstitutionConstants.SCHOOLS_FILTER}&${StoreStateConstants.PAGE}=1` },
      { name: LeftColumnConstants.IP_FORWARDING, pathname: PagePathConstants.IP_FORWARDING_PATH },
      { name: 'Create School', modalType: 'school' },
      { name: 'Create District', modalType: 'district' },
    ],
  },
  {
    name     : LeftColumnConstants.BULK_SMS,
    value    : LeftColumnConstants.BULK_SMS,
    pathname : 'pages',
    children : [
      { name: LeftColumnConstants.BULK_SMS, pathname: PagePathConstants.BULK_SMS },
    ],
  },
  {
    name     : LeftColumnConstants.ENTERPRISE_ACCOUNTS,
    value    : LeftColumnConstants.ENTERPRISE,
    pathname : 'enterprise',
    children : [
      { name: LeftColumnConstants.COUNTRY_ACCOUNTS, pathname: PagePathConstants.COUNTRY_ACCOUNTS_PATH, search: '?page=1' },
    ],
  },
  {
    name     : LeftColumnConstants.ADMIN_TOOLS_TEXT,
    value    : LeftColumnConstants.ADMIN_TOOLS,
    pathname : 'admin_tools',
    children : [
      { name: LeftColumnConstants.INSTITUTION_ADMIN_RIGHTS, pathname: PagePathConstants.ADMIN_INSTITUTION_PATH, search: '?page=1' },
      { name: LeftColumnConstants.TOOLBOX_ADMINS, pathname: PagePathConstants.TOOLBOX_ADMIN_PATH, search: '?page=1' },
    ],
  },
  {
    name     : LeftColumnConstants.DISCOVER,
    value    : LeftColumnConstants.DISCOVER,
    pathname : 'discover',
    children : [
      { name: LeftColumnConstants.FLAGGED, pathname: PagePathConstants.DISCOVER_FLAGGED_PATH },
    ],
  },
  {
    name     : LeftColumnConstants.DDRS,
    value    : LeftColumnConstants.DDRS_MENU,
    pathname : 'ddrs',
    children : [
      { name: LeftColumnConstants.USER_DELETIONS, pathname: PagePathConstants.DDRS_DELETION_PATH, search: '?page=1' },
      { name: LeftColumnConstants.USER_RESTORATIONS, pathname: PagePathConstants.DDRS_RESTORATION_PATH, search: '?page=1' },
    ],
  },
  {
    name     : LeftColumnConstants.NEW_FEATURE_ANNOUNCEMENTS,
    value    : LeftColumnConstants.ANNOUNCEMENT,
    pathname : 'announcement',
    children : [
      { name: LeftColumnConstants.VIEW_ALL_ANNOUNCEMENTS, pathname: PagePathConstants.VIEW_ALL_ANNOUNCEMENTS_PATH, search: '?page=1' },
      { name: LeftColumnConstants.CREATE_NEW_ANNOUNCEMENT, pathname: PagePathConstants.CREATE_ANNOUNCEMENTS_PATH },
    ],
  },
  {
    name     : LeftColumnConstants.ELASTIC_SEARCH,
    value    : LeftColumnConstants.ELASTIC_SEARCH,
    pathname : 'elasticsearch',
    children : [
      { name: LeftColumnConstants.UPSERT_DOCUMENT, pathname: PagePathConstants.ELASTIC_SEARCH_PATH, search: '?page=1&instancePage=1' },
      { name: LeftColumnConstants.ELASTIC_CONFIG_MANAGE, pathname: PagePathConstants.ELASTIC_SEARCH_CONFIG_PATH, search: '?page=1' },
    ],
  },
  {
    name     : LeftColumnConstants.HASHTAGS,
    value    : LeftColumnConstants.HASH_TAGS,
    pathname : 'hash_tags',
    children : [
      { name: LeftColumnConstants.RECOMMEND, pathname: PagePathConstants.HASH_TAGS_RECOMMEND_PATH, search: '?page=1' },
    ],
  },
];

export default menuList;
```

  ```js
   return (
    <div className="left-column">
      <div className="left-header mt-5 mb-3">{leftHeading}</div>

      {menuList.map((item) => {
        const {
          children, name, value, pathname,
        } = item || {};
        const firstLevelMenu = currentUserRbac && currentUserRbac[pathname];

        if (!firstLevelMenu) {
          return null;
        }

        return (
          <Fragment key={name + pathname}>
            <div
              className={collapseClassName(leftCollapse, value, `qa-test-leftcol-${value}`)}
              onClick={() => toggleLeftCollapse(value)}
            >
              {name}
            </div>
            <Collapse isOpen={leftCollapse === value}>
              <Nav vertical>
                {children.map(({
                  pathname, name, callback, search,
                }) => {
                  const [_, secondLevelMenu] = pathname?.slice(1).split('/') || [];
                  const hasAccess = firstLevelMenu?.children[secondLevelMenu];

                  if (callback) {
                    return (
                      <NavLink className={classNames('institution_modal', `qa-test-leftCol-institutions-${camelCase(name)}`)} onClick={callback}>
                        Create School
                      </NavLink>
                    );
                  }

                  if (hasAccess) {
                    return (
                      <NavItem key={pathname + name}>
                        <Link
                          className={`${tabClass(match, pathname)} qa-test-leftCol-superUsers`}
                          to={{ pathname, ...(search && { search }) }}
                        >
                          {name}
                        </Link>
                      </NavItem>
                    );
                  }
                })}
              </Nav>
            </Collapse>
          </Fragment>
        );
      })}
    </div>
  );
  ```
  注意这里面是如何处理菜单模态框的

**5. 获取具体路由模块的操作权限**
> 通过封装一个高阶组件RBACWrapper来判断某一个具体的按钮是否有操作权限，
```js
import react from 'react';
import { connect } from 'react-redux';
import { withRouter } from 'react-router-dom';
import { selectCurrentUserRbacRouteRbac } from '../../selectors/UserSelectors';

const RBACWrapper = ({
  rbacKey, children, location, currentUserRouteRbac,
}) => {
  const { pathname } = location || {};
  const [firstLevelMenu, secondLevelMenu] = pathname && pathname?.slice(1).split('/') || [];

  const currentMenuRbacInfo = currentUserRouteRbac && currentUserRouteRbac[firstLevelMenu]?.children[secondLevelMenu] || [];

  if (!currentMenuRbacInfo.includes(rbacKey)) {
    return null;
  }

  return children;
};

function mapStateToProps(state) {
  return {
    currentUserRouteRbac: selectCurrentUserRbacRouteRbac(state),
  };
}

export default withRouter(connect(mapStateToProps)(RBACWrapper));
```

## Other
- [rbac后端字段对应表](https://shimo.im/sheets/5s64xm0zkT4vCuKy/ZruKR)
- [rbac接口文档](https://edmodoworld-jira.atlassian.net/wiki/spaces/ENG/pages/156270886/API)
- 测试账号
  1. lzy_teacher1@edmodo.com/password superuser_full
  2. lzy_teacher2@edmodo.com/password superuser_customer_support
