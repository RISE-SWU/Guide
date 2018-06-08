

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
            }
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