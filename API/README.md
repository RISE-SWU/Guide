

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
