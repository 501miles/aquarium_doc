# 模型接口定义文档v1.0

## 1.获取鱼缸模型数据

> URL: /tank_model

> Method: POST
> 
> 请求参数:

| 参数名 | 类型 | 必传 | 说明 |
| --- | --- | --- | --- |
| tank_type | int | N | 缸类型枚举: 0->裸缸、2->侧滤缸 |
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
| need_logo | bool | N | 是否打标 |
| logo_location | int | N | 打标位置枚举：0->右上，1->左上，2->左下，3->右下 |
| need_hole | bool | N | 是否打孔 |
| need_stretch | bool | N | 是否拉筋 |
| mark | string | N | 订单备注 |
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

| 参数名 | 类型 | 说明 |
| --- | --- | --- |
| code | int | 状态码: 0->获取成功 |
| msg | string | 消息说明 |
| payload | obj | 数据内容 |
| &emsp;payload.3dmodel | obj_list | 3d数据 |
| &emsp;payload.2dsvg | string | 2d svg数据base64 |



> 请求示例:

```json
{
    "need_hole": true,
    "customer_nickname": "⽤户昵称",
    "draft": false,
    "bottom_thickness": 8,
    "tank_type": 1,
    "mark": "备注",
    "discount": 70,
    "need_stretch": true,
    "logo_location": 0,
    "source": 1,
    "order_no": "202305041003",
    "order_time": 1683832500000,
    "freight": 0,
    "glass_glue_color": 0,
    "sides_thickness": 8,
    "need_logo": true,
    "glass_material_id": 1,
    "length": 600,
    "width": 600,
    "height": 600,
    "btn_comb_distance": 100,
    "stretch_list":
    [
        {
            "stretch_type": 0,
            "vertical_location": 0,
            "vertical_glass_thickness": 8,
            "vertical_count": 2
        }
    ],
    "hole_list":
    [
        {
            "location": 0,
            "diameter": 100,
            "vertical_distance": 100,
            "vertical_location": 0,
            "horizontal_distance": 100,
            "horizontal_location": 0
        }
    ]
}
```
> 响应示例:

```json
{
    "code": 0,
    "msg": "",
    "payload": {
        "3dmodel": [],
        "2dsvg": "data:image/svg;base64,iVBORw0KGgoAAAANSUhEUgAAAU4AAAEVCAMAAAC4xPxvAAADAFBMVEXc5"
    }
}
```

<br/><br/>