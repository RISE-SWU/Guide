

# API文档

## 中文网站后台API

```
//后台用户登录，表RiseUserCN

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