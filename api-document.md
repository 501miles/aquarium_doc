# 接口文档v1.0

接口测试地址: http://www.evan0.xyz:9998/v1/api/${URL}

说明：

> 1.接口请求方式都是POST
>

> 2.请求参数都是application/json
>

> 3.请求响应格式如下
>

| 参数名 | 类型 | 说明 |
| --- | --- | --- |
| code | int | 状态码 |
| msg | string | 消息说明 |
| data | any | 返回的数据 |

示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "name": "nick",
        "token": "xxx"
    }
}
```

> 4.身份验证
>

如果接口需要验证Token，则需要将login接口返回的token设置在请求里，key名称是Authorization

例如:

```json
Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjYwNDgwMTY2MjEwNzQ4NywiaWF0IjoxNjYyMTA3NDg3LCJ1aWQiOjF9.HN5HdfH4Qw18W79--0aqAqyZwr9-r-3Q1PwIYRU3WQs
```

> 5.状态码说明
>

| 状态码定义 | 状态码 | 说明 |
| --- | --- | --- |
| CodeServerNotReady | -3 | 服务器未就绪 |
| CodeDBError | -2 | 数据库错误 |
| CodeSystemError | -1 | 系统错误 |
| CodeOK | 0 | 正常 |
| CodeRequestParamsError | 10 | 请求参数错误 |
| CodeRequestParamsMiss | 11 | 请求参数缺少 |
| CodeInvalidToken | 20 | 非法token |
| CodeInvalidCaptcha | 21 | 验证码错误或过期 |
| CodeWrongUserOrPass | 30 | 用户名或密码错误 |
| CodeUserNotExist | 40 | 用户不存在 |
| CodeUserAlreadyExist | 50 | 用户已存在 |
| CodeUpAlreadyFocus | 60 | up主已关注 |
| CodeDataNotExist | 70 | 数据不存在 |
| CodeDataGetFailed | 80 | 数据获取失败 |
| CodeExportDataFailed | 90 | 数据导出失败 |
| CodeCaptchaGenFailed | 100 | 验证码生成失败 |

## 1.接口健康检查

> URL: /ping

> 需要Token: 否

> 请求参数: 无

> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| status | int | 健康状态，1: ok |

> 请求示例:

```json
{
    
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "status": 1
    }
}
```

<br/><br/>
## 2.登录

> URL: /login

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| username | string | Y | 用户名 |
| password | string | Y | 密码 |
| captcha_id | string | Y | 验证码id |
| captcha_code | string | Y | 验证码 |

> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| name | string | 昵称 |
| token | string | 令牌 |

> 请求示例:

```json
{
    "username": "nick",
    "password": "123456",
    "captcha_id": "HG9bbV9JkEBqoBT8oquY",
    "captcha_code": "963852"
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjYwNDgwMTY2MjEwNzQ4NywiaWF0IjoxNjYyMTA3NDg3LCJ1aWQiOjF9.HN5HdfH4Qw18W79--0aqAqyZwr9-r-3Q1PwIYRU3WQs",
        "name": "nick"
    }
}
```

<br/><br/>
## 3.获取验证码

> URL: /captcha

> 需要Token: 否

> 请求参数: 无

> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| code | string | 验证码 |
| code_id | string | 验证码id |

> 请求示例:


> 响应示例:



<br/><br/>
## 4.重置密码

> URL: /resetPwd

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| old_password | string | Y | 旧密码 |
| new_password | string | Y | 新密码 |

> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 5.保存订单

> URL: /saveOrder

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | 订单id |
| order_time | int | N | 购买日期unix时间戳 |
| order_no | string | N | 订单编号 |
| filter_type | string | N | 缸类型: 裸缸、背滤缸、侧滤缸 |
| draft | bool | N | 是否为草稿 |
| source | string | N | 来源平台 |
| customer_nickname | string | N | 用户昵称 |
| customer_tel | string | N | 用户手机号 |
| length | int | N | 长度(mm) |
| width | int | N | 宽度(mm) |
| height | int | N | 高度(mm) |
| thickness | int | N | 厚度(mm) |
| fish_board_distance_from_bottom | int | N | 鱼梳板打孔距底面高度(mm) |
| color | string | N | 玻璃胶颜色 |
| need_logo | bool | N | 是否打表 |
| logo_location | string | N | 打标位置 |
| need_point | bool | N | 是否打孔 |
| need_steel | bool | N | 是否拉筋 |
| mark | string | N | 订单备注 |
| pic_url | string | N | 产品3D展示图url |
| point_list | object_array | N | 打孔数据 |
| steel_list | object_array | N | 拉筋数据 |

> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 6.改变订单状态草稿<-->正式

> URL: /switchOrder

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |
| type | int | Y | 0草稿 1正式 |

> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 7.查询订单列表

> URL: /searchOrder

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| source | string | N | 来源平台 |
| customer_nickname | string | N | 用户昵称 |
| customer_tel | string | N | 用户手机号 |
| filter_type | string | N | 缸类型: 裸缸、背滤缸、侧滤缸 |
| order_no | string | N | 订单编号 |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |

> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| count | int | 总条数 |
| list | obj_array | 数据列表 |
| &emsp;list.id | int | 订单id |
| &emsp;list.order_time | int | 购买日期unix时间戳 |
| &emsp;list.order_no | string | 订单编号 |
| &emsp;list.filter_type | string | 缸类型: 裸缸、背滤缸、侧滤缸 |
| &emsp;list.draft | bool | 是否为草稿 |
| &emsp;list.source | string | 来源平台 |
| &emsp;list.customer_nickname | string | 用户昵称 |
| &emsp;list.customer_tel | string | 用户手机号 |
| &emsp;list.length | int | 长度(mm) |
| &emsp;list.width | int | 宽度(mm) |
| &emsp;list.height | int | 高度(mm) |
| &emsp;list.thickness | int | 厚度(mm) |
| &emsp;list.fish_board_distance_from_bottom | int | 鱼梳板打孔距底面高度(mm) |
| &emsp;list.color | string | 玻璃胶颜色 |
| &emsp;list.need_logo | bool | 是否打表 |
| &emsp;list.logo_location | string | 打标位置 |
| &emsp;list.need_point | bool | 是否打孔 |
| &emsp;list.need_steel | bool | 是否拉筋 |
| &emsp;list.mark | string | 订单备注 |
| &emsp;list.pic_url | string | 产品3D展示图url |
| &emsp;list.point_list | object_array | 打孔数据 |
| &emsp;list.steel_list | object_array | 拉筋数据 |

> 请求示例:


> 响应示例:



<br/><br/>
## 8.查询订单详情

> URL: /orderDetail

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | N | 订单id |
| order_no | string | N | 订单号 |

> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
