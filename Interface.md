
### 说明
* 专栏的消息均以JSON格式输出
* http method均为GET
* JSON ARRAY 中的数据，只选取了具有代表性的部分进行展示

### 分析

#### 获取指定专栏的文章列表
```
https://zhuanlan.zhihu.com/api/columns/专栏名/posts?limit=数量&offset=从哪里开始
```
例如，获取知乎小管家的最新的10篇文章
```
https://zhuanlan.zhihu.com/api/columns/zhihuadmin/posts?limit=10&offset=0
```
其中，limit为获取的数量限制，offset为偏移量，即从哪里开始获取。
默认数据为limit=10，offset=0，当然你也可以根据需要定义二者的值。
获得的数据为:
```JSON
[
  {
    "isTitleImageFullScreen": false,
    "rating": "none",
    "sourceUrl": "",
    "publishedTime": "2016-10-13T14:00:49+08:00",
    "links":
      {
        "comments": "/api/posts/22921645/comments"
      },
    "author":
      {
        "profileUrl": "https://www.zhihu.com/people/zhihuadmin",
        "bio": "欢迎反馈问题和建议！",
        "hash": "3d198a56310c02c4a83efb9f4a4c027e",
        "uid": 53253479858176,
        "isOrg": false,
        "description": "",
        "slug": "zhihuadmin",
        "avatar":
          {
            "id": "34bf96bf5584ac4b5264bd7ed4fdbc5a",
            "template": "https://pic3.zhimg.com/{id}_{size}.jpg"
          },
        "name": "知乎小管家"
      },
    "url": "/p/22921645",
    "title": "新版社区管理规定于 2016 年 10 月 13 日正式运行",
    "titleImage": "https://pic2.zhimg.com/v2-517f47cc5269b57f26ea4a25f29d8505_r.jpg",
    "summary": "",
    "content": "<p>2016 年 9 月 13 日小管家发布了新版社区管理规定，明确了「恶意行为」的定义和违规类型，同时增加了「发布垃圾广告信息」的 3 种违规类型。在完成了为期 1 个月的试运行后<b>，</b><b><a href=\"https://www.zhihu.com/question/19790711/answer/36685915\" class=\"\" data-editable=\"true\" data-title=\"\u65b0\u7248\u793e\u533a\u7ba1\u7406\u89c4\u5b9a\">\u65b0\u7248\u793e\u533a\u7ba1\u7406\u89c4\u5b9a</a>",
    "state": "published",
    "href": "/api/posts/22921645",
    "meta":
      {
        "previous": null,
        "next": null
      },
    "commentPermission": "anyone",
    "snapshotUrl": "",
    "canComment": false,
    "slug": 22921645,
    "commentsCount": 76,
    "likesCount": 436
  },
]
```

+ isTitleImageFullScreen: 文章标题大图是否全屏
+ rating: ???评级
+ sourceUrl: 源路径
+ publishedTime: 发表时间
+ links: 链接信息
  - comments: 评论地址
+ creator: 该专栏的创建者信息
  - profileUrl: 知乎网的个人主页url
  - bio: 官网信息中的一句话描述
  - hash: hash值
  - uid: uid
  - isOrg: 是否为机构帐号
  - description: 描述
  - slug: slug
  - avatar: 头像信息
    + id: id值，在拼接url时用到
    + template: url拼接模版
  - name: 作者名称
+ url: 文章网页内容获取(https://zhuanlan.zhihu.com + url)
+ title: 文章标题
+ titleImage: 文章标题大图url(需要注意的是,titleImage的值有可能为空)，和头像一样，也可以组合不同的尺寸参数获取不同尺寸的图片
+ summary: 文章简要信息
+ content: HTML格式的文章内容详情，可以通过WebView或者UIWebView展示内容
+ state: 文章状态(是否发表)
+ href: api请求地址

#### 获取评论列表
```
https://zhuanlan.zhihu.com/api/posts/文章slug/comments?limit=数量限制&offset=偏移量
```

这里拼接url的方法和获取文章列表时的方法时一样的，不再赘述。例如获取文章slug为22591792的前30条评论。
```
https://zhuanlan.zhihu.com/api/posts/22591792/comments?limit=30&offset=0
```

获取到的信息为
```JSON
[
  {
    "content": "小管家棒棒哒！支持~",
    "liked": false,
    "href": "/api/posts/22591792/comments/169039008",
    "inReplyToCommentId": 0,
    "reviewing": false,
    "author":
      {
        "profileUrl": "https://www.zhihu.com/people/fei-xiao-gui", "bio": "心中有爱 脚下有风 所以我跑得快~",
        "hash": "41cd5c7249081389da3a523b3cb0629b", "uid": 28048833380352,
        "isOrg": false,
        "description": "品学兼优~",
        "slug": "fei-xiao-gui",
        "avatar":
          {
            "id": "a061ebdd61bb57c81b3206dda51418fc", "template": "https://pic1.zhimg.com/{id}_{size}.jpg"
          },
        "name": "菲小桂"
      },
    "createdTime": "2016-09-23T17:35:54+08:00",
    "featured": false,
    "id": 169039008,
    "likesCount": 1
  }
]
```

+ content: 评论内容
+ liked: 是否给这条评论点过赞
+ href: 该条评论的详情地址
+ inReplyToCommentId: 所回复的评论的id
+ reviewing: 是否正在被审查中
+ author: 评论的作者
  - profileUrl: 知乎网的个人主页url
  - bio: 官网信息中的一句话描述
  - hash: hash值
  - uid: uid
  - isOrg: 是否为机构帐号
  - description: 描述
  - slug: slug
  - avatar: 头像信息
    + id: id值，在拼接url时用到
    + template: url拼接模版
  - name: 作者名称
+ createdTime: 评论创建时间
+ featured: ???是否为精彩评论
+ id: 该条评论的id
+ likesCount: 获得的赞的数量

对他人评论的回复数据有些许的不同，inReplyToCommentId的值不为0，json数据中增加了inReplyToUser字段，内容为author类型。这里不再具体分析。