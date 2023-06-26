# 接口文档v1.0

接口测试地址: http://www.evan0.xyz:9998/v1/api/${URL}

说明：

> 1.常规接口POST请求参数都是application/json
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
| CodeObjError | -4 | 系统错误 |
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
| CodeUserNotActive | 41 | 账户未激活 |
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
| role | int | 角色枚举：1->管理员，2->运营人员，3->销售人员，4->实验员 |
| permit | string | 权限 |

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
## 4.获取系统模块

> URL: /getSystemModules

> Method: POST

> 需要Token: 否

> 请求参数: 无

> 响应参数: obj_list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | 模块id |
| name | string | 模块名称 |
| selectable | bool | 是否可选择 |
| sub_modules | obj_list | 子模块 |

> 请求示例:

```json
{
    
}
```
> 响应示例:

```json
{
    "data": [
        {
            "selectable": false,
            "sub_modules": [
                {
                    "id": 2,
                    "name": "订单列表",
                    "selectable": true,
                    "sub_modules": null
                },
                {
                    "name": "草稿列表",
                    "selectable": true,
                    "sub_modules": null,
                    "id": 3
                }
            ],
            "id": 1,
            "name": "订单管理"
        },
        {
            "sub_modules": [
                {
                    "id": 5,
                    "name": "问题列表",
                    "selectable": true,
                    "sub_modules": null
                }
            ],
            "id": 4,
            "name": "问题管理",
            "selectable": false
        },
        {
            "sub_modules": [
                {
                    "selectable": true,
                    "sub_modules": null,
                    "id": 7,
                    "name": "用户列表"
                }
            ],
            "id": 6,
            "name": "用户管理",
            "selectable": false
        }
    ],
    "code": 0,
    "msg": ""
}
```

<br/><br/>
## 5.保存账号

> URL: /saveAccount

> Method: POST

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | 用户id |
| account | string | Y | 用户名账号 |
| password | string | Y | 密码 |
| name | string | Y | 昵称 |
| role | int | Y | 角色枚举：1->管理员，2->运营人员，3->销售人员，4->实验员 |
| permit | string | Y | 权限 |
| is_active | bool | Y | 是否激活 |


> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 6.账号列表

> URL: /accountList

> Method: POST

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| name | string | N | 昵称 |
| role | int | N | 角色枚举：1->管理员，2->运营人员，3->销售人员，4->实验员 |
| is_active | bool | N | 是否激活 |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| count | int | 总条数 |
| list | obj_array | 数据列表 |
| &emsp;list.id | int | id |
| &emsp;list.created_at | int | 创建时间 |
| &emsp;list.updated_at | int | 更新时间 |
| &emsp;list.last_login_time | int | 上次登录时间unix时间戳 |
| &emsp;list.last_login_ip | string | 上次登录ip |
| &emsp;list.account | string | 账号 |
| &emsp;list.name | string | 用户昵称 |
| &emsp;list.role | int | 角色枚举：1->管理员，2->运营人员，3->销售人员，4->实验员 |
| &emsp;list.permit | string | 权限 |
| &emsp;list.is_active | bool | 是否激活 |

> 请求示例:


> 响应示例:



<br/><br/>
## 7.账号详情

> URL: /accountDetail

> Method: POST

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| account_id | int | Y | 账号id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| created_at | int | 创建时间 |
| updated_at | int | 更新时间 |
| last_login_time | int | 上次登录时间unix时间戳 |
| last_login_ip | string | 上次登录ip |
| account | string | 账号 |
| name | string | 用户昵称 |
| role | int | 角色枚举：1->管理员，2->运营人员，3->销售人员，4->实验员 |
| permit | string | 权限 |
| is_active | bool | 是否激活 |

> 请求示例:


> 响应示例:



<br/><br/>
## 8.重置密码

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
## 9.保存订单

> URL: /saveOrder

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | 订单id |
| order_time | int | N | 购买日期unix时间戳 |
| order_no | string | N | 订单编号 |
| tank_type | int | N | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| draft | bool | N | 是否为草稿 |
| source | int | N | 来源平台枚举：0->抖音，1->快手，2->淘宝，3->微信 |
| customer_nickname | string | N | 用户昵称 |
| length | int | N | 长度(mm) |
| width | int | N | 宽度(mm) |
| height | int | N | 高度(mm) |
| sides_thickness | int | N | 玻璃四面厚度(mm) |
| bottom_thickness | int | N | 玻璃底面厚度(mm) |
| bottom_glass_type | int | N | 玻璃底面类型枚举: 0->单层玻璃，1->双层夹胶玻璃 |
| glass_material_id | int | N | 玻璃材质id |
| btn_comb_distance | int | N | 鱼梳板打孔距底面高度(mm) |
| btn_comb_material_id | int | N | 鱼梳板材质id |
| glass_glue_color | int | N | 玻璃胶颜色枚举：0->透明，1->黑色 |
| discount | int | N | 折扣(0-100) |
| need_logo | bool | N | 是否打标 |
| logo_location | int | N | 打标位置枚举：0->右上，1->左上，2->左下，3->右下 |
| need_hole | bool | N | 是否打孔 |
| need_stretch | bool | N | 是否拉筋 |
| mark | string | N | 订单备注 |
| pic_3d_url | string | N | 产品3D展示图url |
| wooden_frame_price | int | N | 木架价格(分) |
| delivery_address | string | N | 收货详细地址 |
| delivery_province | string | N | 收货地址省 |
| delivery_city | string | N | 收货地址市 |
| delivery_district | string | N | 收货地址区 |
| express_company | int | N | 快递公司枚举：0->顺丰，1->德邦，2->京东 |
| diaphragm_thickness | int | N | 隔板厚mm |
| dry_wet_separation_box_height | int | N | 干湿分离盒高mm |
| filtration_bin_count | int | N | 过滤仓数量 |
| pump_bin | int | N | 泵仓mm |
| filter_material_bin | int | N | 滤材仓mm |
| filter_cotton_bin | int | N | 滤棉仓mm |
| drainage_control_type | int | N | 排水控制枚举: 0->单阀单控，1->多阀多控 |
| diaphragm_type | int | N | 隔板形式枚举: 0->单排隔板，1->双排隔板 |
| diaphragm_bottom_blank | int | N | 隔板下部留空mm |
| diaphragm_height_decline | int | N | 隔板高度递减mm |
| diaphragm_spacing | int | N | 隔板间距mm |
| need_bottom_force | bool | N | 底部强排 |
| bottom_blank | int | N | 底部留高mm |
| need_lid | bool | N | 需要缸盖 |
| dry_wet_sep_box_layer_count | int | N | 干湿分离盒层数 |
| hole_list | object_array | N | 打孔数据 |
&emsp;hole_list.location | int | N | 打孔位置枚举: 0->左侧面，1->右侧面，2->前面，3->后面，4->底面 |
&emsp;hole_list.horizontal_location | int | N | 水平位置枚举: 0->左侧边，1->右侧边 |
&emsp;hole_list.horizontal_distance | int | N | 水平位置距离(mm) |
&emsp;hole_list.vertical_location | int | N | 竖直位置枚举: 0->上侧边，1->下侧边 |
&emsp;hole_list.vertical_distance | int | N | 竖直位置距离(mm) |
&emsp;hole_list.diameter | int | N | 直径(mm) |
| stretch_list | object_array | N | 拉筋数据 |
&emsp;stretch_list.stretch_type | int | N | 拉筋方式枚举: 0->一体拉筋、1->双层拉筋 |
&emsp;stretch_list.vertical_glass_thickness | int | N | 纵拉筋玻璃厚度(mm) |
&emsp;stretch_list.vertical_location | int | N | 纵拉筋位置枚举：0->上，1->下 |
&emsp;stretch_list.vertical_count | int | N | 纵筋数量 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | 订单id |

> 请求示例:

```json
{
    "discount": 70,
    "need_logo": true,
    "glass_material_id": 1,
    "order_no": "202305041003",
    "need_hole": true,
    "logo_location": 0,
    "freight": 0,
    "mark": "备注",
    "hole_list": [
        {
            "location": 0,
            "diameter": 100,
            "vertical_distance": 100,
            "vertical_location": 0,
            "horizontal_distance": 100,
            "horizontal_location": 0
        }
    ],
    "need_stretch": true,
    "height": 600,
    "width": 600,
    "length": 600,
    "source": 1,
    "tank_type": 1,
    "draft": false,
    "stretch_list": [
        {
            "vertical_glass_thickness": 8,
            "vertical_count": 2,
            "stretch_type": 0,
            "vertical_location": 0
        }
    ],
    "glass_glue_color": 0,
    "bottom_glass_type": 0,
    "bottom_thickness": 8,
    "sides_thickness": 8,
    "customer_nickname": "用户昵称",
    "order_time": 1683832500000
}
```
> 响应示例:

```json
{
    "data": {
        "id": 10000
    },
    "code": 0,
    "msg": ""
}
```

<br/><br/>
## 10.查询订单列表

> URL: /searchOrder

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| draft | bool | N | 是否为草稿 |
| source | int | N | 来源平台枚举：0->抖音，1->快手，2->淘宝，3->微信 |
| customer_nickname | string | N | 用户昵称 |
| customer_tel | string | N | 用户手机号 |
| created_time | int | N | 创建时间 |
| tank_type | int | N | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| order_no | string | N | 订单编号 |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| count | int | 总条数 |
| list | obj_array | 数据列表 |
| &emsp;list.id | int | 订单id |
| &emsp;list.created_time | int | 创建时间unix时间戳 |
| &emsp;list.order_time | int | 购买日期unix时间戳 |
| &emsp;list.order_no | string | 订单编号 |
| &emsp;list.tank_type | int | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| &emsp;list.draft | bool | 是否为草稿 |
| &emsp;list.source | int | 来源平台枚举：0->抖音，1->快手，2->淘宝，3->微信 |
| &emsp;list.customer_nickname | string | 用户昵称 |
| &emsp;list.length | int | 长度(mm) |
| &emsp;list.width | int | 宽度(mm) |
| &emsp;list.height | int | 高度(mm) |
| &emsp;list.sides_thickness | int | 玻璃四面厚度(mm) |
| &emsp;list.bottom_thickness | int | 玻璃底面厚度(mm) |
| &emsp;list.bottom_glass_type | int | 玻璃底面类型枚举: 0->单层玻璃，1->双层夹胶玻璃 |
| &emsp;list.glass_material_id | int | 玻璃材质id |
| &emsp;list.btn_comb_distance | int | 鱼梳板打孔距底面高度(mm) |
| &emsp;list.btn_comb_material_id | int | 鱼梳板材质表id |
| &emsp;list.glass_glue_color | int | 玻璃胶颜色枚举：0->透明，1->黑色 |
| &emsp;list.discount | int | 折扣(0-100) |
| &emsp;list.need_logo | bool | 是否打标 |
| &emsp;list.logo_location | int | 打标位置枚举：0->右上，1->左上，2->左下，3->右下 |
| &emsp;list.need_hole | bool | 是否打孔 |
| &emsp;list.need_stretch | bool | 是否拉筋 |
| &emsp;list.mark | string | 订单备注 |
| &emsp;list.pic_3d_url | string | 产品3D展示图url |
| &emsp;list.tank_total_weight | int | 鱼缸总质量（克） |
| &emsp;list.wooden_frame_price | int | 木架价格(分) |
| &emsp;list.delivery_address | string | 收货详细地址 |
| &emsp;list.delivery_province | string | 收货地址省 |
| &emsp;list.delivery_city | string | 收货地址市 |
| &emsp;list.delivery_district | string | 收货地址区 |
| &emsp;list.express_company | int | 快递公司枚举：0->顺丰，1->德邦，2->京东 |
| &emsp;list.final_price | int | 最终价格(分) 折扣价+木架+运费 |

> 请求示例:


> 响应示例:



<br/><br/>
## 11.查询订单详情

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
| created_time | int | 创建时间unix时间戳 |
| order_time | int | 购买日期unix时间戳 |
| order_no | string | 订单编号 |
| tank_type | int | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| draft | bool | 是否为草稿 |
| source | int | 来源平台枚举：0->抖音，1->快手，2->淘宝，3->微信 |
| customer_nickname | string | 用户昵称 |
| length | int | 长度(mm) |
| width | int | 宽度(mm) |
| height | int | 高度(mm) |
| sides_thickness | int | 玻璃四面厚度(mm) |
| bottom_thickness | int | 玻璃底面厚度(mm) |
| bottom_glass_type | int | 玻璃底面类型枚举: 0->单层玻璃，1->双层夹胶玻璃 |
| glass_material_id | int | 玻璃材质id |
| glass_material_name | string | 玻璃材质名称 |
| glass_material_density | string | 玻璃材质密度 |
| btn_comb_distance | int | 鱼梳板打孔距底面高度(mm) |
| btn_comb_material_id | int | 鱼梳板材质id |
| btn_comb_material_name | int | 鱼梳板材质表名称 |
| btn_comb_material_density | int | 鱼梳板材质表密度 |
| glass_glue_color | int | 玻璃胶颜色枚举：0->透明，1->黑色 |
| discount | int | 折扣(0-100) |
| need_logo | bool | 是否打标 |
| logo_location | int | 打标位置枚举：0->右上，1->左上，2->左下，3->右下 |
| need_hole | bool | 是否打孔 |
| need_stretch | bool | 是否拉筋 |
| mark | string | 订单备注 |
| pic_3d_url | string | 产品3D展示图url |
| json_data_3d | string | 3d数据 |
| tank_total_weight | int | 鱼缸总质量（克） |
| wooden_frame_price | int | 木架价格(分) |
| delivery_address | string | 收货详细地址 |
| delivery_province | string | 收货地址省 |
| delivery_city | string | 收货地址市 |
| delivery_district | string | 收货地址区 |
| express_company | int | 快递公司枚举：0->顺丰，1->德邦，2->京东 |
| final_price | int | 最终价格(分) 折扣价+木架+运费 |
| diaphragm_thickness | int | 隔板厚mm |
| dry_wet_separation_box_height | int | 干湿分离盒高mm |
| filtration_bin_count | int | 过滤仓数量 |
| pump_bin | int | 泵仓mm |
| filter_material_bin | int | 滤材仓mm |
| filter_cotton_bin | int | 滤棉仓mm |
| drainage_control_type | int | 排水控制枚举: 0->单阀单控，1->多阀多控 |
| diaphragm_type | int | 隔板形式枚举: 0->单排隔板，1->双排隔板 |
| diaphragm_bottom_blank | int | 隔板下部留空mm |
| diaphragm_height_decline | int | 隔板高度递减mm |
| diaphragm_spacing | int | 隔板间距mm |
| need_bottom_force | bool | 底部强排 |
| bottom_blank | int | 底部留高mm |
| need_lid | bool | 需要缸盖 |
| dry_wet_sep_box_layer_count | int | 干湿分离盒层数 |
| hole_list | object_array | 打孔数据 |
| &emsp;hole_list.location | int | 打孔位置枚举: 0->左侧面，1->右侧面，2->前面，3->后面，4->底面 |
| &emsp;hole_list.horizontal_location | int | 水平位置枚举: 0->左侧边，1->右侧边 |
| &emsp;hole_list.horizontal_distance | int | 水平位置距离(mm) |
| &emsp;hole_list.vertical_location | int | 竖直位置枚举: 0->上侧边，1->下侧边 |
| &emsp;hole_list.vertical_distance | int | 竖直位置距离(mm) |
| &emsp;hole_list.diameter | int | 直径(mm) |
| stretch_list | object_array | 拉筋数据 |
| &emsp;stretch_list.stretch_type | int | 拉筋方式枚举: 0->一体拉筋、1->双层拉筋 |
| &emsp;stretch_list.vertical_glass_thickness | int | 纵拉筋玻璃厚度(mm) |
| &emsp;stretch_list.vertical_location | int | 纵拉筋位置枚举：0->上，1->下 |
| &emsp;stretch_list.vertical_count | int | 纵筋数量 |

> 请求示例:


> 响应示例:



<br/><br/>
## 12.复制产品页

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
| &emsp;item_info.tank_type | int | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| &emsp;item_info.length | int | 长度(mm) |
| &emsp;item_info.width | int | 宽度(mm) |
| &emsp;item_info.height | int | 高度(mm) |
| &emsp;item_info.glass_glue_color | int | 玻璃胶颜色枚举：0->透明，1->黑色 |
| &emsp;item_info.pic_3d_url | string | 产品3D展示图url |
| &emsp;item_info.json_data_3d | string | 3d数据 |
| &emsp;item_info.sides_thickness | int | 玻璃四面厚度(mm) |
| &emsp;item_info.bottom_thickness | int | 玻璃底面厚度(mm) |
| &emsp;item_info.bottom_glass_type | int | 玻璃底面类型枚举: 0->单层玻璃，1->双层夹胶玻璃 |
| &emsp;item_info.glass_material_id | int | 玻璃材质id |
| &emsp;item_info.glass_material_name | string | 玻璃材质名称 |
| &emsp;item_info.glass_material_density | string | 玻璃材质密度 |
| &emsp;item_info.btn_comb_material_id | int | 鱼梳板材质id |
| &emsp;item_info.btn_comb_material_name | int | 鱼梳板材质表名称 |
| &emsp;item_info.btn_comb_material_density | int | 鱼梳板材质表密度 |
| &emsp;item_info.tank_total_weight | int | 鱼缸总质量（克） |
| &emsp;item_info.hole_list | object_array | 打孔数据 |
| &emsp;&emsp;item_info.hole_list.location | int | 打孔位置枚举: 0->左侧面，1->右侧面，2->前面，3->后面，4->底面 |
| &emsp;&emsp;item_info.hole_list.horizontal_location | int | 水平位置枚举: 0->左侧边，1->右侧边 |
| &emsp;&emsp;item_info.hole_list.horizontal_distance | int | 水平位置距离(mm) |
| &emsp;&emsp;item_info.hole_list.vertical_location | int | 竖直位置枚举: 0->上侧边，1->下侧边 |
| &emsp;&emsp;item_info.hole_list.vertical_distance | int | 竖直位置距离(mm) |
| &emsp;&emsp;item_info.hole_list.diameter | int | 直径(mm) |
| &emsp;item_info.stretch_list | object_array | 拉筋数据 |
| &emsp;&emsp;item_info.stretch_list.stretch_type | int | 拉筋方式枚举: 0->一体拉筋、1->双层拉筋 |
| &emsp;&emsp;item_info.stretch_list.vertical_glass_thickness | int | 纵拉筋玻璃厚度(mm) |
| &emsp;&emsp;item_info.stretch_list.vertical_location | int | 纵拉筋位置枚举：0->上，1->下 |
| &emsp;&emsp;item_info.stretch_list.vertical_count | int | 纵筋数量 |
| company_info | obj |  |
| &emsp;company_info.brief_introduction | string | 公司简介 |
| &emsp;company_info.contact | string | 联系人 |
| &emsp;company_info.tel | string | 联系电话 |
| &emsp;company_info.qr_code | string | 二维码 |

> 请求示例:


> 响应示例:



<br/><br/>
## 13.删除订单

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
## 14.保存问题

> URL: /saveQuestion

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | id |
| tank_type | int | Y | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
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
    "tank_type": "裸缸",
    "content": "问题描述内容",
    "relate_category": [
        6,
        7,
        8
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
## 15.查询问题列表

> URL: /searchQuestion

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| key_word | string | N | 关键字 |
| tank_type | int | N | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
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
| &emsp;list.tank_type | int | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| &emsp;list.content | string | 内容 |
| &emsp;list.is_active | bool | 启用状态 |
| &emsp;list.created_time | int | 创建时间 |
| &emsp;list.relate_category | obj_array | 绑定的模块 |
| &emsp;&emsp;list.relate_category.id | int | id |
| &emsp;&emsp;list.relate_category.question_id | int | 问题id |
| &emsp;&emsp;list.relate_category.question_category_id | int | 问题分类id |
| &emsp;&emsp;list.relate_category.question_category_name | string | 问题分类名称 |

> 请求示例:

```json
{
    "page": 1,
    "page_size": 2
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "count": 12,
        "list": [
            {
                "relate_category": [
                    {
                        "id": 35,
                        "question_id": 14,
                        "question_category_id": 6,
                        "question_category_name": "长度"
                    },
                    {
                        "question_id": 14,
                        "question_category_id": 7,
                        "question_category_name": "宽度",
                        "id": 36
                    },
                    {
                        "question_category_id": 8,
                        "question_category_name": "高度",
                        "id": 37,
                        "question_id": 14
                    }
                ],
                "id": 14,
                "created_time": 1682500967,
                "tank_type": "裸缸",
                "content": "问题描述内容",
                "is_active": false
            },
            {
                "id": 13,
                "created_time": 1682500882,
                "tank_type": "裸缸",
                "content": "问题描述内容",
                "is_active": false,
                "relate_category": [
                    {
                        "id": 32,
                        "question_id": 13,
                        "question_category_id": 6,
                        "question_category_name": "是否打标"
                    },
                    {
                        "question_category_id": 7,
                        "question_category_name": "是否打标",
                        "id": 33,
                        "question_id": 13
                    },
                    {
                        "id": 34,
                        "question_id": 13,
                        "question_category_id": 8,
                        "question_category_name": "是否打标"
                    }
                ]
            }
        ]
    }
}
```

<br/><br/>
## 16.问题详情

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
| tank_type | int | 缸类型枚举: 0->裸缸，2->侧滤缸，3->底滤缸 |
| content | string | 内容 |
| is_active | bool | 启用状态 |
| created_time | int | 创建时间 |
| relate_category | obj_array | 绑定的模块 |
| &emsp;relate_category.id | int | id |
| &emsp;relate_category.question_id | int | 问题id |
| &emsp;relate_category.question_category_id | int | 问题分类id |
| &emsp;relate_category.question_category_name | string | 问题分类名称 |

> 请求示例:

```json
{
    "question_id": 14
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "id": 14,
        "created_time": 1682500967,
        "tank_type": "裸缸",
        "content": "问题描述内容",
        "is_active": false,
        "relate_category": [
            {
                "id": 35,
                "question_id": 14,
                "question_category_id": 6,
                "question_category_name": "长度"
            },
            {
                "question_id": 14,
                "question_category_id": 7,
                "question_category_name": "宽度",
                "id": 36
            },
            {
                "id": 37,
                "question_id": 14,
                "question_category_id": 8,
                "question_category_name": "高度"
            }
        ]
    }
}
```

<br/><br/>
## 17.删除问题

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
## 18.获取分享小程序码

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
## 19.获取问题分类

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
## 20.获取玻璃材质分类

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
## 21.获取配置参数

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
## 22.获取标准尺寸鱼缸信息列表

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
## 23.计算当前价格和运费

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
| final_price | int | 最终价格(分) 折扣价+木架+运费 |

> 请求示例:


> 响应示例:



<br/><br/>
## 24.推荐最匹配的标准缸尺寸

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
## 25.获取鱼梳板材质分类

> URL: /getBtnCombMaterial

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
## 26.获取订单pdf路径

> URL: /getOrderPdf

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| order_id | int | Y | 订单id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| pdf_path | string | pdf路径 |

> 请求示例:


> 响应示例:



<br/><br/>
## 27.保存设备温度监测

> URL: /saveDeviceMonitor

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | id |
| device_uuid | string | Y | 温度计序列号 |
| monitor_type | int | Y | 监测类型枚举：0->鱼缸，1->其它 |
| temp_tank_type | int | N | 监测鱼缸类型枚举: 0->海缸，1->淡水缸 |
| tank_status | int | N | 鱼缸状态枚举: 0->新开缸，1->维护中，2->已禁用 |
| length | int | N | 长度mm |
| width | int | N | 宽度mm |
| height | int | N | 高度mm |
| tools_remark | string | N | 使用缸内工具备注 |
| temp_threshold_max | float | N | 最高温度预警阈值 |
| temp_threshold_min | float | N | 最低温度预警阈值 |
| phone_number | string | N | 手机号 |
| sms_notification_limitation_min | int | N | 预警短信通知时效分钟 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |

> 请求示例:


> 响应示例:



<br/><br/>
## 28.设备温度监测查询

> URL: /searchDeviceMonitor

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| monitor_type | int | N | 监测类型枚举：0->鱼缸，1->其它 |
| temp_tank_type | int | N | 监测鱼缸类型枚举: 0->海缸，1->淡水缸 |
| tank_status | int | N | 鱼缸状态枚举: 0->新开缸，1->维护中，2->已禁用 |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |


> 响应参数: obj_list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| created_time | int | 创建时间 |
| device_uuid | string | 温度计序列号 |
| monitor_type | int | 监测类型枚举：0->鱼缸，1->其它 |
| monitor_type | int | 监测类型枚举：0->鱼缸，1->其它 |
| temp_tank_type | int | 监测鱼缸类型枚举: 0->海缸，1->淡水缸 |
| tank_status | int | 鱼缸状态枚举: 0->新开缸，1->维护中，2->已禁用 |
| length | int | 长度mm |
| width | int | 宽度mm |
| height | int | 高度mm |
| tools_remark | string | 使用缸内工具备注 |
| temp_threshold_max | float | 最高温度预警阈值 |
| temp_threshold_min | float | 最低温度预警阈值 |
| phone_number | string | 手机号 |
| sms_notification_limitation_min | int | 预警短信通知时效分钟 |

> 请求示例:


> 响应示例:



<br/><br/>
## 29.设备温度监测详情

> URL: /deviceMonitorDetail

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | Y | id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| created_time | int | 创建时间 |
| device_uuid | string | 温度计序列号 |
| monitor_type | int | 监测类型枚举：0->鱼缸，1->其它 |
| monitor_type | int | 监测类型枚举：0->鱼缸，1->其它 |
| temp_tank_type | int | 监测鱼缸类型枚举: 0->海缸，1->淡水缸 |
| tank_status | int | 鱼缸状态枚举: 0->新开缸，1->维护中，2->已禁用 |
| length | int | 长度mm |
| width | int | 宽度mm |
| height | int | 高度mm |
| tools_remark | string | 使用缸内工具备注 |
| temp_threshold_max | float | 最高温度预警阈值 |
| temp_threshold_min | float | 最低温度预警阈值 |
| phone_number | string | 手机号 |
| sms_notification_limitation_min | int | 预警短信通知时效分钟 |

> 请求示例:


> 响应示例:



<br/><br/>
## 30.删除设备温度监测

> URL: /delDeviceMonitor

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | Y | id |


> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 31.温度统计图表

> URL: /deviceTempStat

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| device_uuid | string | Y | 温度计序列号 |
| start_time | int | N | 起始时间 |
| end_time | int | N | 结束时间 |
| time_type | int | N | 时间维度枚举：0->分，1->时，2->日，3->月 |


> 响应参数: obj_list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| time | int | 时间戳 |
| temperature | float | 温度数据 |

> 请求示例:


> 响应示例:



<br/><br/>
## 32.温度统计数据导出csv

> URL: /exportDeviceTempStat

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| device_uuid | string | Y | 温度计序列号 |
| start_time | int | N | 起始时间 |
| end_time | int | N | 结束时间 |
| time_type | int | N | 时间维度枚举：0->分，1->时，2->日，3->月 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| path | string | 文件路径 |

> 请求示例:


> 响应示例:



<br/><br/>
## 33.保存设备护记录

> URL: /saveDeviceMaintain

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | N | id |
| device_monitor_id | int | Y | 温度监测id |
| time | int | N | 操作时间 |
| operator_account_id | int | N | 操作员id |
| maintain_type | int | N | 维护动作枚举: 0->喂食，1->换水，2->擦缸 |
| pic_path | string | N | 图片路径 |
| mark | string | N | 订单备注 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |

> 请求示例:


> 响应示例:



<br/><br/>
## 34.设备维护查询

> URL: /searchDeviceMaintain

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| page | int | N | 页码，默认1 |
| page_size | int | N | 每页条数，默认20 |


> 响应参数: obj_list

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| device_monitor_id | int | 温度监测id |
| time | int | 操作时间 |
| operator_account_id | int | 操作员id |
| maintain_type | int | 维护动作枚举: 0->喂食，1->换水，2->擦缸 |
| pic_path | string | 图片路径 |
| mark | string | 订单备注 |

> 请求示例:


> 响应示例:



<br/><br/>
## 35.设备维护详情

> URL: /deviceMaintainDetail

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | Y | id |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| id | int | id |
| device_monitor_id | int | 温度监测id |
| time | int | 操作时间 |
| operator_account_id | int | 操作员id |
| maintain_type | int | 维护动作枚举: 0->喂食，1->换水，2->擦缸 |
| pic_path | string | 图片路径 |
| mark | string | 订单备注 |

> 请求示例:


> 响应示例:



<br/><br/>
## 36.删除设备维护记录

> URL: /delDeviceMaintain

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| id | int | Y | id |


> 响应参数: 无

> 请求示例:


> 响应示例:



<br/><br/>
## 37.图片预览

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
## 38.文件下载

> URL: /download

> Method: GET

> 需要Token: 否

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| path | string | Y | 路径 |


> 响应参数: 无

> 请求示例:

```text
?path=pdf/abc.pdf
```
> 响应示例:

```text
FILE_DATA
```

<br/><br/>
## 39.文件上传

> URL: /upload

> Method: POST

> 需要Token: 是

> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| file | form-data file | N | form-data格式的file类型 |


> 响应参数: obj

| 参数名 | 类型  | 说明 |
| --- | --- | --- |
| path | string | 保存的文件路径 |

> 请求示例:


> 响应示例:



<br/><br/>
