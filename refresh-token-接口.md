#### 接口功能

> 获取refresh token

#### URL

> `/api/mobile/v1/auth_token`

#### 格式

> JSON

#### HTTP请求方式

> POST

#### 请求参数

|参数|必选|类型|说明|
|:----|:----|:----|----|
|refresh_token|true|string|refresh_token|

#### 返回字段

|返回字段|字段类型|说明 |
|:----- |:------|:----------------------------- |
|token|string|token 过期时间5分钟|
|refresh_token|string|refresh token 过期时间2小时|
#### 接口示例

>curl -X POST
  http://10.0.0.110:3000/api/mobile/v1/auth_token
  -F refresh_token=eyJhbGciOiJIUz...WxwK-qrFAiGA

```json
{
    "token": "eyJhbG...pQjPWLjGzg",
    "refresh_token": "eyJhbGciO...gZCu-Q"
}
```
