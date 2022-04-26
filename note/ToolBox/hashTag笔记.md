## 表单结构

## 表单数据结构
```js
{
  description: '323523423235235',
  ranked: 17,
  topic_tag_id: 40,
  topic_tag_name: '999',
  related_recommendations: [
    {
      label: '352',
      ranked: 4,
      recommend_type: 'teacher',
      recommended_user_id: 63,
      title: 'TR_D010-tx8-teacher-12352'
    }
  ],
  sticky_posts: [
    {
      post_id: 12,
      label: 'asdasd',
      position: 1
    }
  ]
}
```

## 相关文档
- [hashtag原型图](http://demo.doc.101.com/%E5%9F%83%E5%8F%8AEdmodo%E7%A0%94%E5%8F%91/%E3%80%90ND19275%E3%80%91%E5%9F%83%E5%8F%8AEdmodo%E7%A0%94%E5%8F%91-%E6%94%AF%E6%8C%81%E8%BF%90%E8%90%A5%E7%AE%A1%E7%90%86%E5%8F%8A%E6%89%8B%E5%B7%A5%E6%8E%A8%E8%8D%90Hashtag%E4%B8%8EPost-V1.2/#id=f1gxq5&p=02-1-1_edit_hashtag&g=1)

## 嵌套表单
我觉得hashtag最蛋疼的地方就是嵌套表单这部分， 这部分没有使用真正的嵌套表单  而是使用一种模拟的方式

为什么需要嵌套表单
比如我们编辑Related Recommendation 字段时候， 只有保存才能生效