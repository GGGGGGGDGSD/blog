===========
Sprint-140
--------------------
ANE-143796


route
=================================
reservation/landing
  reservation/landing/search
    reservation/landing/search/detail/1
      reservation/landing/search/detail/1476/form/0
    reservation/search/detail/simple
  reservation/landing/quick
    reservation/landing/quick/form/1


1. Reservation/Form
   reservation/landing/search/detail/1476/form/0 和  reservation/landing/quick/form/:id 其实是共用这个组件

  EventDetail(这部分 form与/quick/form 各用一个)
  ResourceList
  Questions
  WaiverSection
  FeeSummary


```js
const reservationPeriodUnits = {
  NO_OVERRIDE: 0,
  MINUTE: 1, // Date  Time Range / Time Length
  HOUR: 2,  // Date  Time Range / Time Length
  DAY: 3,
  WEEK: 4, // none
  MONTH: 5, // none
  DEFINED_DATE_RANGE: 6,
  RENTAL_BLOCK: 7, // Times slots Date Select
  OVER_NIGHT: 8 // Date Check-in time/Check-out time
};

const reservationUnit = searchDetail.getIn(['generalInformation', 'reservationPeriodUnit']);
在get_facility_detail借口中 generalInformation/reservationPeriodUnit 这个字段下可以取到unit 同时也可以在mock数据中修改这个值达到修改unit的效果

```

------------------------------
[ANE-143913](https://jirafnd.dev.activenetwork.com/browse/ANE-143913)

route:
  http://localhost:7002/jettytest11/reservation/permitcontract/NFplRUFIWDVyZEsyQURoQSsxZDB4dz09?locale=en-US
code path:
  /Users/ysong/project/cui/src/index/modules/PermitContract/index.jsx


body
 Header
 GeneralPermitInfo

 HeaderAndFooter

 customer-info
 RentalChargesSummary
 EventInfo
   BookingSummary
   CustomQuestionAnswer
   WaiverInformation
  
 Deposit
 PaymentRefund
 PaymentSchedules
 Schedule
 Attachment
 Amendment

 HeaderAndFooter
 SignatureLine



Sprint-141
=================

ticket: ANE-142958
-------

test data site:  JT08   teddycon / 1


ANE-144043 - WCAG 2.1 MyAccount - Team Management - Team List - Edit Team
-----------------
source path: TeamEdit/index.jsx
note: 这里使用了这个组件（import { BaseFormItem } from 'shared/components/UserInformationForm';）来处理表单字段 按理说用户相关的表单字段都可以参考这里



ANE-144053 - WCAG 2.1 MyAccount - Team Management - Team List
------------
source path: TeamManagement/index.jsx



ANE-143897 - WCAG 2.1 Home page
---------------
source path: Home/index.jsx



Sprint-141
=================
ticket: ANE-147497



==============
Home>Reservations>Search results [Done]
1. Date and time picker.
  - start time and end time for Time range, After time for Time length
  - Text on Date and time filter after applied Time range. [BE]
  - Text on Date and time filter after applied Time length. [BE]
2. Date and time picker in Check on center map.

Home>Reservations>Search results>Resource detail [Done]
1. Reservation rules [BE]
  - Online reservations open at 11:00 on first accepted advance day.
  - This facility has a fixed check-in time of 2:00 and a fixed check-out time of 11:00.
  - This facility has a fixed check-out time of 11:00.
  - This facility has a fixed check-in time of 2:00.

1. Facility openings calendar
  overnight facility - checkin and checkout time
  specified available time periods for reserve by minute/hour/rental block/
1. Hours of availability
  available time periods for each week days for reserve by week, month[BE]
  [MINUTE]
1. Date and time picker 
   overnight
   - check-in/check-out time
   - search summary. booking pattern [BE]
     API
     rest/reservation/resource/dateranges/summary
     rest/reservation/resource/validation

   - grid cell time when click "open"(PC and table)

  reserve by day facility - search summary

  API
   rest/reservation/resource/timelength/summary

  minute/hour [mock:Facility116457_minutes]
  - start time and end time for Time range, search summary and after time for Time length, 

  rental block 
  - time slots
  - search summary, booking pattern [BE]
  -  grid cell time when hover "open"(PC and table)
  
  week/date range/month

Home>Reservations>Search results>Resource detail>Reservation form [Done]
booking information with time
customer question with answer type as Time



Home>Shopping Cart [Done] only handle same day
  - booking info for reservation transaction.
  
  - Receipt for reservation [需要再在代码中核对一下]
     customer question answer for the question with answer type as Time

Home>Reservations>Quick reservation [Done]
  - Start time and end time in Time range dialog.
  - Column headers for time slots.
  - Text on time slots after the slots were selected.

  - grid cell time on mobile [add]

Home>Reservation>Quick reservation>Quick reservation form. [Done] only handle same day
  - same with Reservation form page.

Home>My Account>Permit search [Done]
  - permit date


Permit contract []
  - Date in permit header
  - Booking start time and end time in Booking summary section
  Question answer for question with answer as Time in Customer Questions section
  Start / End date/Time in Schedules section
  Upload date in Attached files section
  Amendment date, start and end date/time for bookings, question answers in AMENDMENT section
Printed permit/schedule/amendment history

Home>My Account>Permit search>Modify reservation [Done]
booking info for both Legacy and redesign permit.[ 需要再验证Legacy部分]

Home>My account>Transaction history [Done]
transaction time 
===========
```js
import { formattedTimeRangeFunc } from 'shared/translation/formatted';
{ formattedTimeRangeFunc({ startTime, endTime }) }
```
note!!! 对应的WCAG 也要考虑修改


1. 需要后端格式化部分
  - Reservation rules
  - Resource Search(date filter summery on center map)



=============
AWF-2286
------
- [eslint](https://eslint.org/)
主要一下几个点
1. 如何在一个项目中应用eslint https://eslint.org/docs/latest/use/getting-started 
2. 命令行中如何使用eslint 以及对应的参数  package.json中经常使用
3. 配置文件有哪些具体的规则 .eslintrc文件 https://eslint.org/docs/latest/use/core-concepts
4. eslint 搭配vscode具体配置，如何保证在vs code独立应用每个项目的.eslintrc rule  以及自动保存格式化等


==========
PL-482

## 
1. ReactNode、ReactElement区别
2. @faker-js/faker 

## QA
1. detail node api nodeActionType = 1 表示 filling类型？
2. 每次刷新 startinstance只是中间状态？
3. 500 时候页面空白  是否需要自动返回select customer page?


==========
UT-warning
1. Warning: An update to ForwardRef(FormControlHOC) inside a test was not wrapped in act(...).
    
    When testing, code that causes React state updates should be wrapped into act(...):



