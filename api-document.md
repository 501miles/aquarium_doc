# 接口文档v1.0

接口测试地址: http://www.evan0.xyz:9998/v1/api/${URL}

说明：

> 1.POST请求参数都是application/json
>

> 2.POST请求响应格式如下
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

> 3.身份验证
>

如果接口需要验证Token，则需要将login接口返回的token设置在请求里，key名称是Authorization

例如:

```text
Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjYwNDgwMTY2MjEwNzQ4NywiaWF0IjoxNjYyMTA3NDg3LCJ1aWQiOjF9.HN5HdfH4Qw18W79--0aqAqyZwr9-r-3Q1PwIYRU3WQs
```

> 4.状态码说明
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
| CodeDataNotExist | 70 | 数据不存在 |
| CodeDataGetFailed | 80 | 数据获取失败 |
| CodeExportDataFailed | 90 | 数据导出失败 |
| CodeCaptchaGenFailed | 100 | 验证码生成失败 |
| CodeWXQRCodeGenFailed | 110 | 微信小程序二维码生成失败 |

## 1.接口健康检查

> URL: /ping

> Method: POST

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

> Method: POST

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
        "name": "nick",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjYwNDgwMTY2MjEwNzQ4NywiaWF0IjoxNjYyMTA3NDg3LCJ1aWQiOjF9.HN5HdfH4Qw18W79--0aqAqyZwr9-r-3Q1PwIYRU3WQs"
    }
}
```

<br/><br/>
## 3.获取验证码

> URL: /captcha

> Method: POST

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

> Method: POST

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

> Method: POST

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
| length | int | N | 长度(mm) |
| width | int | N | 宽度(mm) |
| height | int | N | 高度(mm) |
| around_thickness | int | N | 玻璃四面厚度(mm) |
| bottom_thickness | int | N | 玻璃底面厚度(mm) |
| glass_material | string | N | 玻璃材质 |
| fish_board_distance_from_bottom | int | N | 鱼梳板打孔距底面高度(mm) |
| color | string | N | 玻璃胶颜色 |
| discount | int | N | 折扣(0-100) |
| need_logo | bool | N | 是否打标 |
| logo_location | string | N | 打标位置 |
| need_point | bool | N | 是否打孔 |
| need_steel | bool | N | 是否拉筋 |
| mark | string | N | 订单备注 |
| pic_url | string | N | 产品3D展示图url |
| point_list | object_array | N | 打孔数据 |
&emsp;point_list.location | string | N | 打孔位置: 左右前后底 |
&emsp;point_list.horizontal | string | N | 水平位置: 距左边测或距右边测 |
&emsp;point_list.horizontal_distance | int | N | 水平位置距离(mm) |
&emsp;point_list.vertical | string | N | 竖直位置: 距上边测或距下边测 |
&emsp;point_list.vertical_distance | int | N | 竖直位置距离(mm) |
&emsp;point_list.diameter | int | N | 直径(mm) |
| steel_list | object_array | N | 拉筋数据 |
&emsp;steel_list.steel_type | string | N | 拉筋方式: 一体拉筋、双层拉筋 |
&emsp;steel_list.glass_thickness | int | N | 纵拉筋玻璃厚度(mm) |
&emsp;steel_list.location | string | N | 纵拉筋位置 |
&emsp;steel_list.count | int | N | 纵筋数量 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | 订单id |

> 请求示例:

```json
{
    "need_point": false,
    "need_steel": false,
    "mark": "sdfsdaf",
    "point_list": [
        {
            "diameter": 789,
            "location": "左",
            "horizontal": "左",
            "horizontal_distance": 1230,
            "rtical": "上",
            "vertical_distance": 456
        },
        {
            "location": "左",
            "horizontal": "左",
            "horizontal_distance": 1230,
            "rtical": "上",
            "vertical_distance": 456,
            "diameter": 789
        },
        {
            "rtical": "上",
            "vertical_distance": 456,
            "diameter": 789,
            "location": "左",
            "horizontal": "左",
            "horizontal_distance": 1230
        }
    ],
    "customer_nickname": "杰克马",
    "height": 333,
    "color": "五彩斑斓",
    "length": 111,
    "fish_board_distance_from_bottom": 555,
    "logo_location": "中间",
    "filter_type": "裸缸",
    "draft": false,
    "customer_tel": "135123456",
    "steel_list": [
        {
            "steel_type": " 一体拉筋",
            "width": 9630,
            "thickness": 852,
            "count": 741
        },
        {
            "steel_type": " 一体拉筋",
            "width": 9630,
            "thickness": 852,
            "count": 741
        },
        {
            "steel_type": " 一体拉筋",
            "width": 9630,
            "thickness": 852,
            "count": 741
        }
    ],
    "source": "aaa",
    "width": 222,
    "thickness": 444,
    "order_time": 1234567890,
    "need_logo": false,
    "pic_url": ""
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "id": 10000
    }
}
```

<br/><br/>
## 6.查询订单列表

> URL: /searchOrder

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| draft | bool | N | 是否为草稿 |
| source | string | N | 来源平台 |
| customer_nickname | string | N | 用户昵称 |
| customer_tel | string | N | 用户手机号 |
| created_time | int | N | 创建时间 |
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
| &emsp;list.created_time | int | 创建时间unix时间戳 |
| &emsp;list.order_no | string | 订单编号 |
| &emsp;list.filter_type | string | 缸类型: 裸缸、背滤缸、侧滤缸 |
| &emsp;list.draft | bool | 是否为草稿 |
| &emsp;list.source | string | 来源平台 |
| &emsp;list.customer_nickname | string | 用户昵称 |
| &emsp;list.length | int | 长度(mm) |
| &emsp;list.width | int | 宽度(mm) |
| &emsp;list.height | int | 高度(mm) |
| &emsp;list.around_thickness | int | 玻璃四面厚度(mm) |
| &emsp;list.bottom_thickness | int | 玻璃底面厚度(mm) |
| &emsp;list.glass_material | string | 玻璃材质 |
| &emsp;list.fish_board_distance_from_bottom | int | 鱼梳板打孔距底面高度(mm) |
| &emsp;list.color | string | 玻璃胶颜色 |
| &emsp;list.discount | int | 折扣(0-100) |
| &emsp;list.price | int | 价格(分) |
| &emsp;list.freight | int | 运费(分) |
| &emsp;list.need_logo | bool | 是否打标 |
| &emsp;list.logo_location | string | 打标位置 |
| &emsp;list.need_point | bool | 是否打孔 |
| &emsp;list.need_steel | bool | 是否拉筋 |
| &emsp;list.mark | string | 订单备注 |
| &emsp;list.pic_url | string | 产品3D展示图url |

> 请求示例:


> 响应示例:



<br/><br/>
## 7.查询订单详情

> URL: /orderDetail

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | N | 订单id |
| order_no | string | N | 订单号 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | 订单id |
| order_time | int | 购买日期unix时间戳 |
| created_time | int | 创建时间unix时间戳 |
| order_no | string | 订单编号 |
| filter_type | string | 缸类型: 裸缸、背滤缸、侧滤缸 |
| draft | bool | 是否为草稿 |
| source | string | 来源平台 |
| customer_nickname | string | 用户昵称 |
| length | int | 长度(mm) |
| width | int | 宽度(mm) |
| height | int | 高度(mm) |
| around_thickness | int | 玻璃四面厚度(mm) |
| bottom_thickness | int | 玻璃底面厚度(mm) |
| glass_material | string | 玻璃材质 |
| fish_board_distance_from_bottom | int | 鱼梳板打孔距底面高度(mm) |
| color | string | 玻璃胶颜色 |
| discount | int | 折扣(0-100) |
| price | int | 价格(分) |
| freight | int | 运费(分) |
| need_logo | bool | 是否打标 |
| logo_location | string | 打标位置 |
| need_point | bool | 是否打孔 |
| need_steel | bool | 是否拉筋 |
| mark | string | 订单备注 |
| pic_url | string | 产品3D展示图url |
| point_list | object_array | 打孔数据 |
| &emsp;point_list.location | string | 打孔位置: 左右前后底 |
| &emsp;point_list.horizontal | string | 水平位置: 距左边测或距右边测 |
| &emsp;point_list.horizontal_distance | int | 水平位置距离(mm) |
| &emsp;point_list.vertical | string | 竖直位置: 距上边测或距下边测 |
| &emsp;point_list.vertical_distance | int | 竖直位置距离(mm) |
| &emsp;point_list.diameter | int | 直径(mm) |
| steel_list | object_array | 拉筋数据 |
| &emsp;steel_list.steel_type | string | 拉筋方式: 一体拉筋、双层拉筋 |
| &emsp;steel_list.glass_thickness | int | 纵拉筋玻璃厚度(mm) |
| &emsp;steel_list.location | string | 纵拉筋位置 |
| &emsp;steel_list.count | int | 纵筋数量 |

> 请求示例:


> 响应示例:



<br/><br/>
## 8.复制产品页

> URL: /showItem

> Method: POST

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| item_info | obj |  |
| &emsp;item_info.filter_type | string | 缸类型: 裸缸、背滤缸、侧滤缸 |
| &emsp;item_info.length | int | 长度(mm) |
| &emsp;item_info.width | int | 宽度(mm) |
| &emsp;item_info.height | int | 高度(mm) |
| &emsp;item_info.color | string | 玻璃胶颜色 |
| &emsp;item_info.pic_url | string | 产品3D展示图url |
| company_info | obj |  |
| &emsp;company_info.brief_introduction | string | 公司简介 |
| &emsp;company_info.contact | string | 联系人 |
| &emsp;company_info.tel | string | 联系电话 |
| &emsp;company_info.qr_code | string | 二维码 |

> 请求示例:


> 响应示例:



<br/><br/>
## 9.删除订单

> URL: /delOrder

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 10.保存问题

> URL: /saveQuestion

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | id |
| aquarium_type | string | Y | 鱼缸类型 |
| content | string | Y | 内容 |
| is_active | bool | N | 启用状态 |
| relate_category | int_array | Y | 绑定的模块 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | 问题id |

> 请求示例:

```json
{
    "aquarium_type": "裸缸",
    "content": "问题描述内容",
    "relate_category": [
        1,
        2,
        3
    ]
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "id": 11
    }
}
```

<br/><br/>
## 11.查询问题列表

> URL: /searchQuestion

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| key_word | string | N | 关键字 |
| aquarium_type | string | N | 鱼缸类型 |
| is_active | bool | N | 启用状态 |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| count | int | 总条数 |
| list | obj_array | 数据列表 |
| &emsp;list.id | int | 问题id |
| &emsp;list.created_time | int | 创建时间 |
| &emsp;list.aquarium_type | string | 鱼缸类型 |
| &emsp;list.content | string | 内容 |
| &emsp;list.is_active | bool | 启用状态 |
| &emsp;list.created_time | int | 创建时间 |

> 请求示例:


> 响应示例:



<br/><br/>
## 12.问题详情

> URL: /questionDetail

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| question_id | int | Y | 问题id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| aquarium_type | string | 鱼缸类型 |
| content | string | 内容 |
| is_active | bool | 启用状态 |
| created_time | int | 创建时间 |
| relate_category | int_array | 绑定的模块 |

> 请求示例:


> 响应示例:



<br/><br/>
## 13.删除问题

> URL: /delQuestion

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| question_id | int | Y | 问题id |


> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 14.获取分享小程序码

> URL: /getShareWXAppCode

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| qrcode_path | string | 二维码路径 |

> 请求示例:


> 响应示例:



<br/><br/>
## 15.获取问题分类

> URL: /getQuestionCategory

> Method: POST

> 需要Token: 是

> 请求参数: 无

> 响应参数: obj_array

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| name | string | 类型名 |
| parent_id | int | 父级id |
| selectable | bool | 是否可选 |
| sub_category | obj_array | 子类型 |

> 请求示例:


> 响应示例:



<br/><br/>
## 16.获取玻璃材质分类

> URL: /getGlassMaterial

> Method: POST

> 需要Token: 是

> 请求参数: 无

> 响应参数: list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| name | string | 类型名 |
| density | string | 密度 |

> 请求示例:


> 响应示例:



<br/><br/>
## 17.获取配置参数

> URL: /getConfigData

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| key | string | N | 配置数据key |


> 响应参数: list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| name | string | key名 |
| config_data | string | 配置数据 |

> 请求示例:


> 响应示例:



<br/><br/>
## 18.获取标准尺寸鱼缸信息列表

> URL: /getStandardAquariumList

> Method: POST

> 需要Token: 是

> 请求参数: 无

> 响应参数: list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| length | int | 长度(mm) |
| width | int | 宽度(mm) |
| length | int | 高度(mm) |
| thickness | int | 厚度(mm) |
| price | int | 价格(分) 100=1元 |

> 请求示例:


> 响应示例:



<br/><br/>
## 19.计算当前价格和运费

> URL: /calculatePrice

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| calculated_price | int | 当前尺寸计算出的价格(分) |
| freight | int | 运费(分) |

> 请求示例:


> 响应示例:



<br/><br/>
## 20.推荐最匹配的标准缸尺寸

> URL: /recommendAquarium

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| recommend_length | int | 推荐长度(mm) |
| recommend_width | int | 推荐宽度(mm) |
| recommend_height | int | 推荐高度(mm) |
| recommend_thickness | int | 推荐厚度(mm) |
| recommend_price | int | 推荐价格(分) 100=1元 |

> 请求示例:


> 响应示例:



<br/><br/>
## 21.图片预览

> URL: /preview

> Method: GET

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| path | string | Y | 路径 |


> 响应参数: 无

> 请求示例:

```text
?path=3cT9XtF1nJtD/2501681355694.jpg
```
> 响应示例:

```text
IMAGE_DATA
```

<br/><br/>
