# express相关问题

## 跨域问题

直接配置

```javascript
//设置允许跨域访问该服务.
app.all("*",function (req,res,next) { 
  res.header("Access-Control-Allow-Origin","*");
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
  res.header("X-Powered-By",' 3.2.1');
  res.header("Content-Type", "application/json;charset=utf-8");
  next();
});
```



使用cors处理跨域

cors文档地址：https://www.npmjs.com/package/cors

```javascript
npm install cors
const express = require('express')
const cors = require('cors')
const app = express()
app.use(cors())
```



环境：前端vue / axios 后台express/express-session 

备注：后台在使用前两种方式配置跨域请求后 axios发送请求后,能正常发起请求但是后台不能获取express-session的值，而使用接口测试时发现能获取到session

本地跨域

```javascript
app.all('*', function (req, res, next) {
  // 根据需要配置http://localhost:8080的值，vue cli 默认8080端口
  res.header("Access-Control-Allow-Origin", "http://localhost:8080");
    
  res.header("Access-Control-Allow-Credentials", "true");
  res.header("Access-Control-Allow-Headers", "Content-Type,Content-Length, Authorization, Accept,X-Requested-With");
  res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
  res.header("X-Powered-By",' 3.2.1')
  if(req.method=="OPTIONS") res.send(200);/*让options请求快速返回*/
  else  next();
})
```

