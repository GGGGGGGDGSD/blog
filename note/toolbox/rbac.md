## rbac前端设计与记录
 ### 实现效果
 1. 不同的用户看到不同的菜单
 2. 页面之间跳转到没权限访问的路由友好显示为not fund页面
 3. 手动在地址栏输入没权限访问的路由友好显示为not fund页面
 ### 核心思路
  1. 数据结构
  > 从前端的角度，加载应用后首先展示的就是菜单，然后在通过菜单导航到具体页面，这意味着需要获得一个菜单级别（路由级别）的权限表，其次是页面级别的权限表以及一个角色表
  - 菜单级别权限表决定菜单如何展示，以及路由渲染
  - 页面级别权限表决定页面具体的按钮是否展示 可操作等
  - 角色表目前很少。如果能拿到当前用户的具体操作权限，至于是什么角色其实我们可以不用关心，正是基于此，没怎么使用角色，后面可能会考虑辅助控制具体页面级别的bottom
  
  2. 关联
  - 需要控制Route路由渲染, 菜单渲染，拿到具体路由的权限，能关联这些只有路由地址，所以路由会成为后面关联各种操作的核心节点
  - 需要保证路由地址的唯一性。我们目前应用的菜单基本都是二级菜单，所有我们把一级路由+二级路由 作为一个操作权限模块（保证唯一性）
  - 三级路由通过地址拿到二级路由的具体操作权限操作

 ### 具体实现
  > 具体实现前一些思考
   - 如何知道哪些菜单是展示 哪些隐藏
   - 如何知道当前菜单有哪些具体的权限
   - 如何把Route LeftColumn（menu）渲染和rbacKey关联起来


   4. 计算菜单级别的权限表
     配置rbac路由映射表routeRbacMap, 配置规则：通过[这个表](https://shimo.im/sheets/5s64xm0zkT4vCuKy/ZruKR)计算对应rbacKey对应的路由(目前只考虑到二级路由)
     
     ```js
     // key = rbacKey  value = url
     const routeRbacMap = {
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
   5. 路由级别的权限表结构。最终放进状态管理的是下面第二种结构，因为这种结构更方便后面使用
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
     1. 最外层的key代表第一级路由
     2. children 代表子菜单
     3. children里面的key代表第二级路由
   
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

3. 路由渲染权限控制
  > 通过高阶组件ProtectedRoute来渲染可访问的路由
  具体逻辑：通过Route组件传递进来的参数pathname计算得到第一级路由和第二级路由，通过这两个参数以及权限表可判断当前路由是否可访问
  ```js
    const [first, second] = path?.slice(1)?.split('/') || [];
    const hasAccessInfo = currentUserRouteRbac && currentUserRouteRbac[first]?.children[second];
  ```

4. 菜单渲染
  > 核心逻辑和上面一样
  ```js
    const [firstMenu, secondLevelMenu] = pathname?.slice(1).split('/') || [];
    const hasAccess = firstLevelMenu?.children[secondLevelMenu];
  ```
  注意这里面是如何处理菜单模态框的

5. 获取具体路由模块的操作权限
