## 环境问题
- Gemfile ruby '2.6.2'
- Gemfile gem 'mysql2', '>= 0.5.3', '< 0.6.0' 
- gem 'wdm', '>= 0.1.0'
- webpack.yml check_yarn_integrity: false 关闭检测
- 下面这些文件不能提交
1 Gemfile Gemfile.lock
2 db目录相关
3 config目录相关
4 note.md

> 这两个文件的本地修改也不要提交了

## 设置命令行代理
```bash
  set HTTP_PROXY=http://127.0.0.1:1080(设置后直接有效)
  
```

## 用到还没完全掌握技术
- immutable
- reselect

## 技术
### 数据流处理
-  axios + redux + immutable + reselect

### 一些约定
### 关于常量
- 全部提取到对应的constants常量配置文件

### 关于一些公共方法
- 全部提取到对应模块的helper文件

## 样式处理
- scss
- 内部是使用了bootstrap的样式文件  所以可以使用bootstrap 提供的类名 所以可以在这个页面(https://getbootstrap.com/docs/4.6/utilities/borders/) 查询可以使用的类名



## 一些业务问题

> 创建district或者school时候  由于没有重名检测机制  查询会返回所有的同名的数据 前端获取第一条  而且更新是依赖name(这也是一个问题)
> 查询district 或者school 如果输入数字  变成检索条数去查询（是一个问题
> 基础组件复用问题


## 培训
玩了四年游戏 几乎不能正常毕业  留级一年 自学半年编程 入行 

如何开一家咖啡店
1 目标用户
2 产品卖点点
3 

卖什么：产品定位,产品特色， 差异化优势竞品
怎么卖：渠道，宣传，搞活动，店面装修风格
卖给谁： 目标用户

## auto reloading
- webpacker.yaml修改
  hmr项改为true

- 移除编译文件
 删除public目录下packs文件夹

- run webpack-dev-server
  ruby bin/webpack-dev-server

- run server
  rails s -p 3005

- github token 
   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


### 账号
用户名 yi@edmodo.com 
密码  123456

### 
- luojiang  192.168.218.131:3000
- luoyongmao  https://api-edmodo.dazebot.dev
- lizhengyu   http://192.168.218.63:3000

#### 环境变量
```shell
export ONE_EYE_BASE_URL=https://api-edmodo.dazebot.dev
export GOOGLE_CLIENT_ID=952695565802-7bec5mr7sfm16giis6ibnr2f8umlhi3b.apps.googleusercontent.com
export GOOGLE_CLIENT_SECRET=9IGNTy8C4KkxZqh3ZflzpjA4
export ONE_EYE_CLIENT_ID=cb3c6d7de3566391afc267233e62452aa05a7f3b49572475f1588c75d477066c
export ONE_EYE_CLIENT_SECRET=ee15fb82d76b3af080db3aa3c3b4390d66c954dfa923751f4528cf7eb3a69c33
============================== luo jiang
export GOOGLE_CLIENT_ID=952695565802-7bec5mr7sfm16giis6ibnr2f8umlhi3b.apps.googleusercontent.com
export GOOGLE_CLIENT_SECRET=9IGNTy8C4KkxZqh3ZflzpjA4
export ONE_EYE_BASE_URL=http://192.168.218.131:3000
export ONE_EYE_CLIENT_ID=f5c2c12abab099d734410ef291e4025188179d0363cb60d7365854c5b8622244
export ONE_EYE_CLIENT_SECRET=b6d6834345a6c4936743716c6ff24ef5434922cd0c7e90fc298de3d3c05f2db1

=============================zheng yu
export GOOGLE_CLIENT_ID=952695565802-7bec5mr7sfm16giis6ibnr2f8umlhi3b.apps.googleusercontent.com
export GOOGLE_CLIENT_SECRET=9IGNTy8C4KkxZqh3ZflzpjA4
export ONE_EYE_CLIENT_ID=1725195a8ff60be4785eb5f89699a8b46a44132615d462e5597b168886babe00
export ONE_EYE_CLIENT_SECRET=d3a78b2c5be1ebb168d16029b308498ac0017496b6ec1e8b7e964e9e2b492df1
export ONE_EYE_BASE_URL=http://192.168.218.60:3000



========================nanfeng
  GOOGLE_CLIENT_ID = "339378826083-d69i9392rjjmmeil82mpm8l4rpfq1qfj.apps.googleusercontent.com"
  GOOGLE_CLIENT_SECRET = "JK5EYVaXYZjgJAh0kgl5eVzC"
  clientId : 'ce5f74da3582951ca8942c3f2a37aeb380ab82acba896885149d04b6591778a9',
  client_secret=404f84f83f49afd5f23f7e33788c43e01a96cc60909338318a33ec3c0e26ca70
  baseUrl : 'http://192.168.218.53:3000',


```


========================================= secrets.yml

  # google_client_id: <%= ENV['GOOGLE_CLIENT_ID'] %>
  google_client_id: 339378826083-d69i9392rjjmmeil82mpm8l4rpfq1qfj.apps.googleusercontent.com
  # google_secret:  <%= ENV['GOOGLE_CLIENT_SECRET'] %>
  google_secret: JK5EYVaXYZjgJAh0kgl5eVzC
  secret_key_base: 14766ee2d23674791400322ab1a13178c80ff255c7b5277b7b647a1f511d2bf70983c40f21a9e76ec396fde6f948b709acf2ac52a37b342c3250ca128f460c67
  bugsnag_api_key: <%= ENV['BUGSNAG_API_KEY'] %>
  # one_eye_client_id: <%= ENV['ONE_EYE_CLIENT_ID'] %>
  one_eye_client_id: ce5f74da3582951ca8942c3f2a37aeb380ab82acba896885149d04b6591778a9
  # one_eye_client_secret:  <%= ENV['ONE_EYE_CLIENT_SECRET'] %>
  one_eye_client_secret:  404f84f83f49afd5f23f7e33788c43e01a96cc60909338318a33ec3c0e26ca70
  clever_client_id: <%= ENV['CLEVER_CLIENT_ID'] %>
  clever_client_secret:  <%= ENV['CLEVER_CLIENT_SECRET'] %>
  aws_access_key_id: <%= ENV["AWS_ACCESS_KEY_ID"] %>
  aws_secret_access_key: <%= ENV["AWS_SECRET_ACCESS_KEY"] %>

## todo
1. manage gmail
2. learn about edmodo wiki study
3. learn about work flow(Jira git)
4. learn about immutable.js

## 流程
1. 及时更改ticket状态
2. 如果ticket依赖后端，需要Link相关链接
3. 如果ticket依赖后端, IN QA 需要备注在merge这个之前需要先merge相关后端ticket(参考https://edmodo.atlassian.net/browse/TBOX-1025)
This ticket has dependency with BE work. Please CHECK BE branch xxx merged/ before merge this ticket’s PR

// classflow
课前 课中 课后  目前我们课中比较弱（业务功能）

QAmerge 


const device = selector(state, 'Device');
const selector = formValueSelector(StoreStateConstants.CREATE_NEW_ANNOUNCEMENT_FORM);
array.push(StoreStateConstants.CREATE_NEW_ANNOUNCEMENT_FORM, createAnnouncementFormConstants.LANGUAGE, language);


{
    "bullet_points": [
        {
            "id": 2,
            "bullet_point_id": 2,
            "language": "en-US",
            "content": "hahahahah",
            "header": "hehehehhe"
        }
    ],
    "release_date": "2021-04-20T12:22:42.000Z",
    "ios_version": null,
    "administrators": true,
    "android_version": "7.1.1",
    "parents": true,
    "name": "campaign2",
    "teachers": true,
    "status": "active",
    "web": true,
    "updated_at": "2021-04-02T10:22:58.000Z",
    "modifier": {
        "gender": null,
        "premium_type": null,
        "parent_code": null,
        "user_enrollment_group_id": null,
        "unread_chat_messages": null,
        "profile_sub_subject_id": null,
        "unused_rights_15": null,
        "profile_subject_id": null,
        "unused_rights_16": null,
        "country_id": null,
        "subject_ids": null,
        "premium_expires_at": null,
        "alternative_school": null,
        "ads_eligible": true,
        "school_id": null,
        "admin_rights": null,
        "other_relationship": null,
        "date_of_birth": null,
        "display_name": null,
        "state_id": null,
        "learning_style_id": null,
        "email_verified": true,
        "vanity": "teacherfirst1-teacherlast1",
        "teaching_start_year": null,
        "representative_user_type": "regular",
        "district_id": 1,
        "about": null,
        "parent_relationship": null,
        "creation_date": 1609956251,
        "user_type": 1,
        "sync_merged": false,
        "secondary_email": null,
        "current_user": null,
        "last_login_at": "2021-05-17T06:56:11.000Z",
        "coppa_verified": true,
        "start_level_id": "pre_kindergarten",
        "attributes_changed_by_setter": {},
        "super_user_level": "admin",
        "last_name": "TeacherLast1",
        "role": 0,
        "username": "teacher1",
        "admin_rights_list": null,
        "secondary_email_verified": null,
        "premium": null,
        "verified_institution_member": true,
        "title": 3,
        "language": 0,
        "translator": false,
        "avatars": {
            "small_avatar_url": "https://u.ph.edim.co/default-avatars/1_42.jpg",
            "large_avatar_url": "https://u.ph.edim.co/default-avatars/1_140.jpg",
            "next_avatar_url": "https://u.ph.edim.co/c4ca/1_1_140.png"
        },
        "end_level_id": "higher_education",
        "first_name": "TeacherFirst1",
        "bulk_created": false,
        "id": 1,
        "mutations_from_database": {},
        "password": null,
        "user_subjects": null,
        "career_id": null,
        "email": "zhengyu@edmodo.com",
        "sync_enabled": false,
        "time_zone": null,
        "community_verified": null
    },
    "students": true,
    "images": [
        "https://u.ph.edim.co/default-avatars/1_42.jpg"
    ],
    "id": 2
}


// 一个个人配置记录

- git config 配置
别名  代理 

- nvm 
  node 版本管理

- npm
 常用全局包  包远  以及npn config 

 - vscode 
  个人vscode 配置 以及  常用插件（icon  path提示  tailwind  css属性提示 lint  

- sublime
因为轻量级 所以使用 常用个人配置





