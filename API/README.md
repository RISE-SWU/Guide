


# API文档

## 中文网站后台API
### 后台用户登录，表RiseUserCN，访问地址 '/'
```
Method: 
    post
Request:
    url: /api/validAdmin/
    data: {
        user: 'xxx',
        password: 'xxx',
        /*0代表登陆的是管理员，1代表登陆的是老师及学生用户*/
        type: 0 | 1 
    }
Response: 
    {
       type: 'success' | 'error',
       /*只有error状态才会返回status字段，0代表账号和密码不匹配，1代表账号不存在*/
       status: 0 | 1 
    }

``` 
### 后台账号管理页面，表RiseUserCN，访问地址'/main/account'
```
Method:
    get
Request:
    url: /api/account/
Response:
    {
        status: 'success' | 'error'
        /*success情况下返回dataList*/
        dataList: [
            {   
                id: 12,
                user: 'xxx',
                password: 'ccc',
                type: 0,
                createTime: '2012-01-17'
            },
            {
                id: 2,
                user: 'xxff',
                password: 'fcc',
                type: 1,
                createTime: '2015-08-17'
            },
            ...
        ]
   }
    
```

### 账号添加功能，访问地址'/main/account'

```
Method: 
    post

Request: 
    url: /api/account/add
    data: {
        user: 'xxx',
        password: 'xxx',
        type: 0, 
        createTime: '2014-02-21'
    }

Response:
    {
        //后台要判断是否数据库中已经有该用户名，如果有的话创建失败返回error
        status: 'success' | 'error',
        newData: {
            id: 23,
            user: 'xxx',
            password: 'xxx',
            type: 0,
            createTime: '2014-02-21'
        }
    }
```

### 密码变更功能，访问地址/main/account

```
Method: 
    Post

Request:
    url: /api/account/update
    data: {
        id: 23,
        password: 'xxxxx'
    }

Response: 
    {
        status: 'success' | 'error',
    }
```

### 用户删除功能，访问地址/main/account

```
Method:
    Post

Request:
    url: /api/account/delete
    data: {
        id: 23,
    }
Response:
    {
        status: 'success' | 'error'  
    }

```

## <hr></hr>

## 建表newsListCn

字段 | 类型 | 说明 | 例子
------------ | ------------- | ------------ | -------------
id | Interger | 主键，自增 | 23
title | String | 新闻标题 | 'xxxxxxx'
author | String | 新闻发布者 | 'rise_admin'
tag | String | 新闻标签 | '出访'
status | Interger | 发布状态 | 0或者1
createTime | String | 新闻创建时间 | '2012-09-21'
uploadTime | String | 新闻发布时间 | '2015-05-23'
views | Interger | 该新闻访问人数 | 223
待续 | 待续 | 待续 | 待续

### 新闻列表展示，访问地址： /main/news

```
    Method:
        get
    Request:
        url: /api/news
    Response:
        data: {
            status: 'success',
            dataList: [
                {
                    author:"towguryiac",
                    createTime:"1981-07-02",
                    id:1,
                    status:1,
                    tag:"成权",
                    title:"队系还响种声拉六思建产得青究市院",
                    uploadTime:"2002-01-13",
                },
                {
                    author:"towgFc",
                    createTime:"1911-07-02",
                    id:23,
                    status:0,
                    tag:"试试",
                    title:"队系还GV兜风思建产得青究市院",
                    uploadTime:"2008-01-13",
                },
                ...
            ]
        }
```
### 新闻批量删除/批量发布

```
    Method: 
        Post
    Request:
        删除url: /api/news/delete
        发布url: /api/news/upload

        data: [
            {
                author:"towguryiac",
                createTime:"1981-07-02",
                id:1,
                status:1,
                tag:"成权",
                title:"队系还响种声拉六思建产得青究市院",
                uploadTime:"2002-01-13",
            },
            {
                author:"towgFc",
                createTime:"1911-07-02",
                id:23,
                status:0,
                tag:"试试",
                title:"队系还GV兜风思建产得青究市院",
                uploadTime:"2008-01-13",
            },
        ],
    Response: 
        data: {
            status: 'success' | 'error'
        }
```


## <hr></hr>

### 后台管理页面首页，访问地址'/main/'

```
    Method: 
        Get
    Request:
       url: 
            /api/getIndex
    Response: 
        data {
            status: 'success' | 'error',
            dataList: {
                total: {
                    //发布的新闻总数
                    news: 20,
                    //管理员账户数量
                    admin: 23,
                    //用户账户数量
                    account: 52
                    //头图数量
                    picture: 25
                },
                //记录最近登录的5个账号
                inspect: [
                    {
                        //账号类型
                        type: 0 | 1,
                        userName : 'rise_admin',
                        date: 2017-05-21,
                        time: xx-xx-xx
                    },
                    ...
                ],
                //最近发布的10条新闻
                activity: [
                    {
                        title： 'ccccccc',
                        author: 'xxxxx',
                        uploadTime: 'xxxx-xx-xx',
                        id: 21
                    }   
                ]
            }
        }
    
```
<hr />

### 新闻发布 / 编辑页面，访问地址 /main/edit?id=xx

页面信息显示，id为-1代表新建一篇新闻，此时不会发出请求

```
    Method: 
        Get
    Request:
        Url:
            /api/news/edit?id=xxx
    Response:
        data: {
                status: 'success',
                news: {
                    title: 'xxxxx',
                    author: 'rise_admin',
                    tag: '出访',
                    createTime: '2015-12-03',
                    content: `<p style="color: red">一条大财后</p>`,
                    uploadTime: '2018-09-08'
                }
            }
```

图片上传

```
    Method:
        post
    Request:
        url
            /api/upload/image
        data
            FormData类型的图片
            multipart/form-data; boundary=----WebKitFormBoundaryzArATUyyahlOCQlC
    Response:
        data {
            url: './xx/xx/xx.jpg' //服务器上可以直接访问的图片地址，需要跨域
        }

```
文章信息发布、保存
```
Method: 
    Post
Request:
    url
        /api/news/publish
    data: {
        newsDetail: {
            type: -1 | 0
            content: 'xxx',
            id: 3,
            tag: 'xxx',
            author: 'xxx',
            title: 'xxx'
        }
    }
    //-1 代表保存新闻，不发布， 0代表直接发布，后台需要自己将创建时间和发布时间保存到数据库，如果类型是-1代表是保存新闻，这时候更新createTime字段并保存，并将发布时间重置为空，如果是0的话，更新uploadTime字段并保存，如果是新建新闻并直接发布，此时createTime和uploadTime保持一致并保存到数据库
Response:
    data: {
        status: 'success'
    }
```

