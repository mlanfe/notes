#### 原理

http协议的工作流程

http协议请求信息和响应信息的格式

请求:

- 请求行	

  - 请求方法: GET POST HEAD PUT DELETE TRACE OPTIONS...

    - HEAD和GET基本一致, 只是返回内容

  - 请求路径: 也就是请求的资源，是url的一部分

  - 所用协议

    

- 请求头信息

  - 格式：key: value

  - 请求头信息结束后要空一行, 来分隔头信息和主体信息，即使没有主体信息，也要空行

  - 对于post请求，要在头信息里面规定请求主体的长度  `Content-Length：<Num>` 和请求主体类型`Content-Type:<string>`

    

- 请求主体信息（可选）: post请求比get请求多请求主体信息



响应

- 响应行: 协议版本 状态码 状态文字

- 响应头信息

  - 格式：key: value
  - 其中响应头信息里的Content-Length表示响应主体的长度
  - 响应头信息结束后有一个空行，来分隔头信息和主体信息

- 响应主体信息（可选）

  

#### 实战

#### 优化





