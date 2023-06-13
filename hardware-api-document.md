# 硬件数据上报接口

## 说明：

>1. POST请求参数都是application/json
>
>1. 请求头里设置参数Authorization: e9zbZzTMZ0bIKAn6
>
>1. 接口测试地址前缀http://evan0.xyz:9998/v1/api

## 1.温度计数据上报

> URL: /thermometer_report

> Method: POST
> 
> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| device_uuid | string | Y | 温度计设备唯一id |
| temperature | int | Y | 温度数值 |


> 响应参数: obj

| 参数名 | 类型 | 说明 |
| --- | --- | --- |
| code | int | 状态码: 0:请求成功 |
| msg | string | 消息说明 |
| data | obj | 返回参数 |


> 请求示例:

```json
{
    "device_uuid": "95d9f2b3-2a10-4d90-a627-3266fcdac49b",
    "temperature": "26"
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "data":{}
}
```

<br/><br/>