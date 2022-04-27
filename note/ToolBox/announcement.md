## 整体来说  announcement功能就是围绕创建，编辑， 展示表单数据。所以基本都是表单操作

## 表单数据结构
```js
{
  'en-US': [
    {
      id: 99,
      content: '333333',
      header: '3333333'
    },
    {
      id: 102,
      content: '222222222',
      header: '111111111'
    }
  ],
  
  it: [
    {
      id: 100,
      content: 'uuuuuuuuuuuuu',
      header: 'uuuuu'
    }
  ],
  name: 'Back2school2021======oooooooooooooooooo',
  zh: [
    {
      id: 101,
      content: 'lllllllllllll',
      header: 'llllll'
    }
  ],
  scheduleTime: '16:10',
  release_date: '2022-04-22T08:10:00.000Z',
  teachers: true,
  status: 'active',
  Device: 'web',
  version: 1,
  images: [
    'https://ed.dev.mes1.edme.be/2/NNi0wpyrLWwzov5P.jpg'
  ],
}
```

## 表单操作
1. 绑定表单字段
2. 设置默认值
3. 验证警告提示
4. 表单字段联动
5. 表单与Tab切换（重点关注redux-form提供的FieldArray）
6. 表单提交

### 表单提交成功后具体导航到哪个状态的tab
```js
/* where to go  after request success

                                     create                    edit

                            scheduled   draft       active   scheduled   draft

 Publish                    scheduled   draft       active   scheduled   scheduled

 Save as Draft
No, Save as Draft           draft       draft       draft       draft     draft

 Cancel                      /           /              go where from
*/
```

### 表单编辑
> 注意各种数据的转换
```js
static getInitForm(announcement) {
  if (Map.isMap(announcement)) {
    const release_date = new Date(this.getReleaseDate(announcement));
    const scheduleTime = `${release_date?.getHours()?.toString()?.padStart(2, '0')}:${release_date?.getMinutes()?.toString()?.padStart(2, '0')}`;
    const [Device, version] = this.getInitFormDevice(announcement) || [];
    const bulletMap = this.getInitFormBulletMap(announcement);

    const initForm = {
      id           : this.getId(announcement),
      name         : this.getName(announcement),
      release_date,
      scheduleTime,
      Device,
      version,
      teachers     : true,
      status       : this.getStatus(announcement),
      images       : this.getImage(announcement),
      bulletPoints : this.getInitBulletMap(announcement),
    };

    return fromJS(initForm).merge(bulletMap);
  }
}
```

### 表单更新提交
> 这里单独拿出来主要是因为后端提供更新（编辑）接口不是全量覆盖之前数据，而是只提交变动的那部分数据，这意味着在更改一个announcement时候需要对比, 代码如下

```js
static getCompareCampaignParams(oldForms, newForms) {
  if (Map.isMap(oldForms) && Map.isMap(newForms)) {
    const compareFields = [
      createAnnouncementFormConstants.NAME,
      createAnnouncementFormConstants.TEACHERS,
    ];

    const compareResult = compareFields.reduce((accum, field) => {
      if (oldForms.get(field) !== newForms.get(field)) {
        accum[field] = newForms.get(field);

        return accum;
      }
      return accum;
    },
    {});

    if (
      oldForms.get(createAnnouncementFormConstants.RELEASE_DATE) !== newForms.get(createAnnouncementFormConstants.RELEASE_DATE)
      || oldForms.get(createAnnouncementFormConstants.SCHEDULE_TIME) !== newForms.get(createAnnouncementFormConstants.SCHEDULE_TIME)
    ) {
      compareResult.release_date = this.getCreateReleaseDate(newForms);
    }

    if (
      oldForms.get(createAnnouncementFormConstants.DEVICE) !== newForms.get(createAnnouncementFormConstants.DEVICE)
      || oldForms.get(createAnnouncementFormConstants.VERSION) !== newForms.get(createAnnouncementFormConstants.VERSION)
    ) {
      const platform = newForms.get(createAnnouncementFormConstants.DEVICE);
      const oldPlatform = oldForms.get(createAnnouncementFormConstants.DEVICE);
      compareResult[platform] = platform !== createAnnouncementFormConstants.WEB ? parseInt(newForms.get(createAnnouncementFormConstants.VERSION)) : 1;
      // the device is checkbox, so unselected device require reset to '0';
      compareResult[oldPlatform] = 0;
    }
    return compareResult;
  }
}
```

### 图片处理
> 图片处理流程是这样：前端提交图片到s3然后得到图片的url, 这个url是我们需要存贮到服务器数据库的数据。当前图片还有以下可以优化

1. 在提交表单时候才上传图片。提交表单的请求顺序是：上传图片到s3成功后得到url => 再发送创建/编辑announcement的请求
2. 当前更改没有提供更新图片 这部分需要先调通删除图片成功的相关s3配置

## 文档资源
- [接口文档]（https://shimo.im/docs/kqtHjVy39xVp8Xvy/read）