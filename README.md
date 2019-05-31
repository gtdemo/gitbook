---
description: APP使用接口列表
---

# igps

{% hint style="warning" %}
调用成功时`Status Code 返回200，返回值需要移除首尾XML字符串`

调用失败时`Status Code 返回500，服务器错误，不需要处理返回`
{% endhint %}

{% api-method method="post" host="" path="/Appservice.asmx/Login" %}
{% api-method-summary %}
Login
{% endapi-method-summary %}

{% api-method-description %}
登录并获得loginKey以调用后续其他接口
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="LoginType" type="integer" required=true %}
登录账号类型 0:账户 1:车牌
{% endapi-method-parameter %}

{% api-method-parameter name="UserName" type="string" required=true %}
账号
{% endapi-method-parameter %}

{% api-method-parameter name="UserPswd" type="string" required=true %}
密码
{% endapi-method-parameter %}

{% api-method-parameter name="OSType" type="integer" required=true %}
系统类型 0:安卓 1:IOS
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"Data": {
		"Status": "1",
		"Type": "0",   // 0:账号登录 1:车牌登录
		"Msg": "8888", // 用户名/车牌号
		"ObjectID": "666", // 用户ID/设备ID
		"SF": "0",
		"LoginKey": "43F4532BD2DDE638414B16A255A73DB6" // 后续接口调用凭证
	}
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="密码错误" %}
```javascript
{
	"Data": {
		"Status": "0",
		"Msg": "账号或密码错误",
		"LoginKey": ""
	}
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="用户过期" %}
```javascript
{
	"Data": {
		"Status": "0",
		"Msg": "用户过期",
		"LoginKey": ""
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/WxHomeData" %}
{% api-method-summary %}
WxHomeData
{% endapi-method-summary %}

{% api-method-description %}
获取首页统计数量
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=true %}
zh:中文 en:英文
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,  // 错误码 0:成功
	"errMsg": "ok.", // 错误消息
	"total": null, 
	"data": {
		"errCode": 0,
		"errMsg": null,
		"lowBatteryCount": 0, // 低电报警数量(单位：辆)
		"fallOffCount": 0,    // 拆机报警
		"cutOffCount": 0,     // 剪线报警
		"regionCount": 0,     // 区域报警
		"simExpiredCount": 0, // SIM卡过期
		"onlineRate": 0,      // 有线设备在线率
		"overOfflineCount": 100, // 无限设备离线超过3天
		"recentAddedCount": 9    // 最近90天新增数量
	}
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="无效凭证" %}
```javascript
{
	"errCode": -1, // 错误码 -1:无效凭证
	"errMsg": "Loginkey invalid.",
	"total": null,
	"data": null   // 无效时data为null.
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/WxSpeical\_GetHoldName" %}
{% api-method-summary %}
WxSpeical\_GetHoldName
{% endapi-method-summary %}

{% api-method-description %}
获取用户节点信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="holdId" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="showCount" type="integer" required=true %}
是否显示设备数量 0:显示 1:不显示
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": {
		"id": 6666,    // 用户ID
		"name": "6666",// 用户名
		"count": 0,     // 设备数量
		"isLeaf": false // 是否有子用户
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/WxSpeical\_GetNodeList" %}
{% api-method-summary %}
WxSpeical\_GetNodeList
{% endapi-method-summary %}

{% api-method-description %}
获取用户子节点信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="holdId" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="showCount" type="integer" required=true %}
是否显示设备数量 0:显示 1:不显示
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 3,
	"data": [{
		"id": "11064", // 用户ID
		"name": "001", // 用户名
		"count": 0,    // 设备数量
		"isLeaf": false// 是否有子用户
	}, {
		"id": "11084",
		"name": "002",
		"count": 0,
		"isLeaf": true
	}, {
		"id": "11085",
		"name": "003",
		"count": 0,
		"isLeaf": false
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
部分接口参数含有复杂数据类型时

Headers需要增加Contet-type:application/json，Body需要上传json对象

调用成功时，需要从返回的json字符串的属性d中获取返回值

例：查询车辆列表 QueryVehicleList

Headers: Content-Type:application/json

Body:{ "loginKey": "43F4532BD2DDE638414B16A255A73DB6", "pageIndex": 1, "pageSize": 10, "sortKey": "", "sortDirect": "", "filters": \[\], "holdIDs": \[\], "typeID": 0 }

返回：{ "d": "返回值”}
{% endhint %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/Appservice.asmx/QueryVehicleList" %}
{% api-method-summary %}
QueryVehicleList
{% endapi-method-summary %}

{% api-method-description %}
查询车辆列表
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="pageIndex" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="pageSize" type="integer" required=true %}
数量
{% endapi-method-parameter %}

{% api-method-parameter name="sortKey" type="string" required=true %}
排序关键字，可空
{% endapi-method-parameter %}

{% api-method-parameter name="sortDirect" type="string" required=true %}
排序方向，可空
{% endapi-method-parameter %}

{% api-method-parameter name="filters" type="array" required=true %}
过滤条件，可空数组，车牌、SIM卡号、设备ID模糊查找：\[ { "PropertyName": "MIX", "Value": "关键字", "Operation": 0 }\]
{% endapi-method-parameter %}

{% api-method-parameter name="holdIDs" type="array" required=true %}
所属用户范围，可为空数组
{% endapi-method-parameter %}

{% api-method-parameter name="typeID" type="integer" required=true %}
0：全部，1：在线，2：离线，3：报警，4：未用，5：关注
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"total": 1,
	"list": [{
		"VehicleID": 103831,                // 车辆ID        
		"HoldID": 12077,                    // 用户ID
		"ObjectID": 133017,                 // 设备ID
		"VehicleName": "谷德80222001631",    // 车牌
		"RiskScore": null,                  // 风险分值
		"LendPeopleID": null,               // 车主ID
		"LendPeopleName": "",               // 车主名称
		"Status": 1,                        
		"isOnline": true,                   // 是否在线
		"isAlarm": false,                   // 是否报警
		"isFocus": false,                   // 是否关注
		"RcvTime": "2019-03-08 09:51:13",   // 接收时间
		"TypeID": [1, 2],                   // 状态数组 1 所有 2 在线 3 离线 4 报警 5 未用 6 关注
		"desc": "25Days",                   // 离线时长
		"list": [{                          // 车辆安装的设备列表
			"ObjectID": 133017,                // 设备ID
			"VehicleID": 103831,
			"HoldID": 12077,
			"ObjectType": 3137,                // 设备类型
			"ObjectTypeName": "",              // 类型名称
			"TrackerType": 0,                  // 有线 0 无线 1
			"TrrackerTypeName": "Assets Tracker",   // 有线无线名称
			"SIM": "17241382183",              // SIM卡号
			"SIM2": "80222001631",             // 设备ID
			"ObjectName": "0 谷德80222001631",  
			"RcvTime": "2019-03-08 09:51:13",  // 接收时间
			"GPSTime": "2019-03-08 09:51:12",  // 定位时间
			"Status": 1,                       // acc状态
			"isAlarm": false,                  // 是否报警
			"isOnline": true,                  // 是否在线
			"isVip": true,                     // 是否VIP
			"MDTTypeID": 20,                   // 设备协议类型ID
			"desc": "25Days"                   // 离线时长
		}]
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/Appservice.asmx/QueryTrackDataByVehicleID" %}
{% api-method-summary %}
QueryTrackDataByVehicleID
{% endapi-method-summary %}

{% api-method-description %}
查询设备实时数据（使用VehicleID）
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="vehicleID" type="integer" required=true %}
车辆ID
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}
语言，"zh"或者"en", 可空，默认"zh"
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
    "errCode": 0,
    "errMsg": "ok.",
    "total": 3,
    "data": [
        {
            "id": "220453",
            "vehicle": "2011161120",
            "objecttype": "1",
            "status": "",
            "gpstime": "",
            "rcvtime": "",
            "lon": "",
            "lat": "",
            "rlon": "0",
            "rlat": "0",
            "speed": "",
            "direct": "",
            "directDesc": "",
            "mile": "0.0",
            "statusdes": "从未上线",
            "isalarm": "",
            "remainDays": "0",
            "endDate": "2019-03-27 16:19:33",
            "holdName": null,
            "extData": null,
            "mdtTypeID": "10",
            "mdtTypeName": "vdf",
            "payEndDate": "2019-03-29 00:00:00",
            "address": null,
            "sim": "101000948514",
            "Battery": "0",
            "BatteryLife": "0",
            "TrackerType": "1",
            "sim2": "101000948514",
            "TodayMile": null,
            "Schedule": ""
        },
        {
            "id": "86229",
            "vehicle": "2011161120",
            "objecttype": "1",
            "status": "0",
            "gpstime": "2017-06-30 10:50:45",
            "rcvtime": "2017-06-30 10:51:24",
            "lon": "114.964027",
            "lat": "30.222918",
            "rlon": "114.969159392147",
            "rlat": "30.2202846156124",
            "speed": "102.0",
            "direct": "56",
            "directDesc": "东北",
            "mile": "0.0",
            "statusdes": "行驶,卫星13,定时回传",
            "isalarm": "0",
            "remainDays": "0",
            "endDate": "2025-11-26 14:34:54",
            "holdName": null,
            "extData": null,
            "mdtTypeID": "21",
            "mdtTypeName": "vdf2",
            "payEndDate": "2051-11-26 14:34:54",
            "address": "湖北省鄂州市大塘角西南379米",
            "sim": "21110009450",
            "Battery": "0",
            "BatteryLife": "0",
            "TrackerType": "0",
            "sim2": "1010009450",
            "TodayMile": null,
            "Schedule": ""
        },
        {
            "id": "40247",
            "vehicle": "2011161120",
            "objecttype": "1",
            "status": "0",
            "gpstime": "2017-11-15 18:37:57",
            "rcvtime": "2017-11-15 18:38:07",
            "lon": "113.941995",
            "lat": "22.556118",
            "rlon": "113.946870967865",
            "rlat": "22.5531014614472",
            "speed": "0.0",
            "direct": "0",
            "directDesc": "向北",
            "mile": "15.0",
            "statusdes": "启动怠速[2分6秒],主电压13.9V,GSM强29,卫星中5,回传[13秒]",
            "isalarm": "0",
            "remainDays": "0",
            "endDate": "2021-11-14 00:00:00",
            "holdName": null,
            "extData": null,
            "mdtTypeID": "10",
            "mdtTypeName": "vdf",
            "payEndDate": "2035-12-27 00:00:00",
            "address": "广东省深圳市琼宇路附近科苑学里东北30米",
            "sim": "1302001589",
            "Battery": "0",
            "BatteryLife": "0",
            "TrackerType": "0",
            "sim2": "1302001589",
            "TodayMile": null,
            "Schedule": ""
        }
    ]
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="失败" %}
```javascript
{
    "errCode": 40001,
    "errMsg": "无数据",
    "total": null,
    "data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryTrackDataByObjectIDs" %}
{% api-method-summary %}
QueryTrackDataByObjectIDs
{% endapi-method-summary %}

{% api-method-description %}
查询设备实时数据（使用ObjectID数组）
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="objectIDs" type="array" required=true %}
设备ID数组
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 2,
	"data": [{
		"id": "86229",        // ObjectID
		"vehicle": "摩拜单车1",// 车牌
		"objecttype": "1",    // 车辆类型
		"status": "0",        // ACC状态 1:ACC开 0:ACC关
		"gpstime": "2017-06-30 10:50:45",// GPS时间
		"rcvtime": "2017-06-30 10:51:24",// 接收时间
		"lon": "114.964027",  // 经纬度，wgs84
		"lat": "30.222918",
		"rlon": "114.969159392147", // 纠偏经纬度 gcj-02
		"rlat": "30.2202846156124",
		"speed": "102.0", // 速度 km/h
		"direct": "56", // 方向 0-360 正北方向顺时针 0：正北 90：正东 180：正南 270：正西
		"directDesc": "东北",// 方向描述
		"mile": "0.0", // 总里程 km
		"statusdes": "行驶,卫星13,定时回传",// 设备状态
		"isalarm": "0", // 是否报警 1:报警  0:未报警
		"remainDays": "10047",// 有效日期剩余天数
		"endDate": "2023-11-26 14:34:54",
		"holdName": null,
		"extData": null,
		"mdtTypeID": "21",   // 协议ID
		"mdtTypeName": "vdf2", // 协议名
		"payEndDate": "2046-11-26 14:34:54", // 付费有效期
		"address": "湖北省鄂州市大塘角西南379米", // 地址
		"sim": "21110009450", // SIM卡号码
		"Battery": "0", // 电池电量百分比
		"BatteryLife": "0", // 电池预计剩余可用时间
		"TrackerType": "0", // 0:有线设备 1:无限设备
		"sim2": "1010009450", // 设备ID
		"Schedule": "", // 设备回传时间点
		"TodayMile": null // 当日0点里程
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/WxSpeical\_SearchUser2" %}
{% api-method-summary %}
WxSpeical\_SearchUser2
{% endapi-method-summary %}

{% api-method-description %}
关键字查找用户
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="downloadMd5" type="string" required=true %}
同loginKey
{% endapi-method-parameter %}

{% api-method-parameter name="key" type="string" required=true %}
查找关键字
{% endapi-method-parameter %}

{% api-method-parameter name="size" type="string" required=true %}
分页数量
{% endapi-method-parameter %}

{% api-method-parameter name="mode" type="string" required=true %}
1:全匹配 2:模糊查询
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
[{
	"value": "001", // 用户名
	"id": "11064",  // 用户ID
	"parentHoldId": "10040", // 上级用户ID
	"count": 1 // 用户设备数量
}, {
	"value": "002",
	"id": "11084",
	"parentHoldId": "10040",
	"count": 0
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/WxSpeical\_AddFocusCar" %}
{% api-method-summary %}
WxSpeical\_AddFocusCar
{% endapi-method-summary %}

{% api-method-description %}
用户关注车辆
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="downloadMd5" type="string" required=true %}
同 loginKey
{% endapi-method-parameter %}

{% api-method-parameter name="ObjectId" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```
0
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/WxSpeical\_DeleteFocusCar" %}
{% api-method-summary %}
WxSpeical\_DeleteFocusCar
{% endapi-method-summary %}

{% api-method-description %}
用户取消关注
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="downloadMd5" type="string" required=true %}
同loginKey
{% endapi-method-parameter %}

{% api-method-parameter name="ObjectId" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```
0
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/WxSpeical\_GetTableCount" %}
{% api-method-summary %}
WxSpeical\_GetTableCount
{% endapi-method-summary %}

{% api-method-description %}
获取 用户名下不同状态的车辆数量
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="downloadMd5" type="string" required=true %}
同 loginKey
{% endapi-method-parameter %}

{% api-method-parameter name="holdId" type="array" required=true %}
用户ID数组
{% endapi-method-parameter %}

{% api-method-parameter name="showChild" type="boolean" required=true %}
是否包含下级 true:包含 false:不包含
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"totalCount": 15,// 总数量
	"onlineCount": 0,// 在线数量
	"offlineCount": 15,// 离线数量
	"unusedCount": 4, // 未用数量
	"onalarmCount": 0,// 报警数量
	"focusCount": 0 // 关注数量
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/GetAlarmList" %}
{% api-method-summary %}
GetAlarmList
{% endapi-method-summary %}

{% api-method-description %}
获取报警信息列表
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="key" type="string" required=true %}
关键词
{% endapi-method-parameter %}

{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="page\_size" type="integer" required=true %}
每页数量
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"Data": {
		"RowCount": "2",   // 本次返回数量
		"TotalCount": "2", // 总数量
		"List": [{
			"ObjectID": "201669", 
			"ObjectName": "潜伏_013", // 车牌
			"AlarmType": "低电压报警", // 报警类型
			"ObjectType": "1",        // 设备类型
			"RcvTime": "2019/5/25 15:30:02" // 接收时间
		}, {
			"ObjectID": "201670",
			"ObjectName": "潜伏_014",
			"AlarmType": "低电压报警",
			"ObjectType": "1",
			"RcvTime": "2019/5/25 15:29:54"
		}]
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/CancelAlarm" %}
{% api-method-summary %}
CancelAlarm
{% endapi-method-summary %}

{% api-method-description %}
取消报警
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="ObjectID" type="integer" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"Data": {
		"RowCount": "1" // 1:取消成功 0:取消失败
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/GetTrackData" %}
{% api-method-summary %}
GetTrackData
{% endapi-method-summary %}

{% api-method-description %}
获取轨迹数据
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="ObjectID" type="integer" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="StartTime" type="string" required=true %}
起始时间：yyyy-MM-dd HH:mm:ss
{% endapi-method-parameter %}

{% api-method-parameter name="EndTime" type="string" required=true %}
结束时间
{% endapi-method-parameter %}

{% api-method-parameter name="Speed" type="integer" required=true %}
最小速度 km/h
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"Data": {
		"RowCount": "240",
		"List": [{
			"GPSTime": "2019/5/24 15:05:29", // GPS时间
			"RcvTime": "2019/5/24 15:05:38", // 接收时间
			"Lon": "113.941897", // 经纬度 wgs84
			"Lat": "22.557463",
			"Speed": "0.0", // 速度
			"Direct": "320", // 方向
			"Mileage": "8.0", // 里程
			"Alarm": "1", // 是否报警 1:报警 0:未报警
			"Status": "1", // ACC状态 1:ACC开 0:ACC关
			"Reversal": "0", // 
			"GPSFlag": "1", // 是否GPS定位 奇数:GPS定位 偶数：非GPS定位
			"StatusDes": "启动怠速,回传,低电压报警,LTE网络强31,卫星强8,主电压3.6V,电量7%,定位模式:卫星定位优先,休眠模式,回传间隔6分钟,SIM卡ICCID898602B52616C2388304",
			"rLon": "113.946772938439", // 纠偏经纬度 gcj-02
			"rLat": "22.5544464052941",
			"DirectDes": "西北" // 方向描述
		}]
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/WxGetNodeInfo" %}
{% api-method-summary %}
WxGetNodeInfo
{% endapi-method-summary %}

{% api-method-description %}
获取父级信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="holdId" type="string" required=true %}
用户ID
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"value": "0.研发测试", // 用户名
	"id": "17",      // 用户ID
	"parentHoldId": 17, // 上级用户ID，与用户ID相同时则为当前账号根用户
	"count": 2368 // 用户设备数量
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/WxParkList" %}
{% api-method-summary %}
WxParkList
{% endapi-method-summary %}

{% api-method-description %}
获取长停点数据
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="objectId" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=true %}
最小停留时间\(分钟\)
{% endapi-method-parameter %}

{% api-method-parameter name="from" type="string" required=true %}
开始时间 yyyy-MM-dd HH:mm:ss
{% endapi-method-parameter %}

{% api-method-parameter name="to" type="string" required=true %}
结束时间 yyyy-MM-dd HH:mm:ss
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": [{
		"CarName": null, 
		"UserName": null,
		"ObjectId": null,
		"Place": "广东省深圳市龙大高速公路附近老虎坳西北173米", // 未知
		"StartTime": "2019-05-23 00:01:23", // 开始停放时间
		"EndTime": "2019-05-23 14:37:47", // 结束停放时间
		"ParkMinutes": "14小时36分", // 停车时长
		"Lon": 113.96377998129167, // 经纬度
		"Lat": 22.6883173095348
	}, {
		"CarName": null,
		"UserName": null,
		"ObjectId": null,
		"Place": "广东省深圳市龙大高速公路附近老虎坳西北166米",
		"StartTime": "2019-05-23 20:40:35",
		"EndTime": "2019-05-24 08:46:50",
		"ParkMinutes": "12小时6分",
		"Lon": 113.96399437727661,
		"Lat": 22.688417840077424
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/GetTripData" %}
{% api-method-summary %}
GetTripData
{% endapi-method-summary %}

{% api-method-description %}
获取行程数据
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="objID" type="string" required=true %}
ObjectID
{% endapi-method-parameter %}

{% api-method-parameter name="startTime" type="string" required=true %}
起始 时间:  yyyy-MM-dd HH:mm:ss
{% endapi-method-parameter %}

{% api-method-parameter name="endTime" type="string" required=true %}
结束 时间: yyyy-MM-dd HH:mm:ss
{% endapi-method-parameter %}

{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"data": [{
		"starttime": "2019/05/25 08:44:39", // 行程开始时间
		"endtime": "2019/05/25 09:47:19", // 行程结束时间
		"mileages": 27.9, // 行驶里程
		"startplace": "广东省深圳市龙大高速公路附近福大利五金制品有限公司东北138米",
		"endplace": "广东省深圳市铜鼓路附近科苑学里东北67米",// 起始位置
		"slonlat": "113.958840,22.691287", // 起点经纬度
		"elonlat": "113.942610,22.555992", // 终点经纬度
		"timeSpan": "1小时2分" // 用时
	}, {
		"starttime": "2019/05/25 10:11:20",
		"endtime": "2019/05/25 11:26:43",
		"mileages": 24.5,
		"startplace": "广东省深圳市铜鼓路附近科苑学里东北64米",
		"endplace": "广东省深圳市龙大高速公路附近福大利五金制品有限公司东北133米",
		"slonlat": "113.942615,22.555997",
		"elonlat": "113.958795,22.691293",
		"timeSpan": "1小时15分"
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/WxSaveUserInfo" %}
{% api-method-summary %}
WxSaveUserInfo
{% endapi-method-summary %}

{% api-method-description %}
修改用户密码
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="oldPassword" type="string" required=true %}
旧密码
{% endapi-method-parameter %}

{% api-method-parameter name="newPassword" type="string" required=true %}
新密码
{% endapi-method-parameter %}

{% api-method-parameter name="RealName" type="string" required=true %}
姓名
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok."
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Appservice.asmx/GetPushFlag" %}
{% api-method-summary %}
GetPushFlag
{% endapi-method-summary %}

{% api-method-description %}
获取报警推送开关设置，各标志位对应开关参考下图。  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"WXPushFlag": "BFFFFFFF", // 推送开关
	"MainPushFlag": "1" // 推送总开关
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

![&#x63A8;&#x9001;&#x5F00;&#x5173;&#x6807;&#x5FD7;&#x4F4D;](.gitbook/assets/image%20%282%29.png)

{% api-method method="post" host="" path="/Appservice.asmx/SetPushFlag" %}
{% api-method-summary %}
SetPushFlag
{% endapi-method-summary %}

{% api-method-description %}
设置报警推送开关
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="LoginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="wxPushFlag" type="string" required=true %}
开关详细 8位16进制字符串，如:BFFFFFFF
{% endapi-method-parameter %}

{% api-method-parameter name="mainPushFlag" type="string" required=true %}
推送总开关 0: 不推送 1:推送
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```
{
	"Rows": "1", // 1:保存成功 0:保存失败
	"WXPushFlag": "BFFFFFFF",
	"MainPushFlag": "1"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryDevice" %}
{% api-method-summary %}
QueryDevice
{% endapi-method-summary %}

{% api-method-description %}
查询设备列表
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-type" type="string" required=true %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="pageIndex" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="pageSize" type="integer" required=true %}
页面数量
{% endapi-method-parameter %}

{% api-method-parameter name="sortKey" type="string" required=true %}
排序字段、可为空字符串
{% endapi-method-parameter %}

{% api-method-parameter name="sortDirect" type="string" required=true %}
排序方向、可为空字符串
{% endapi-method-parameter %}

{% api-method-parameter name="filters" type="array" required=true %}
查找条件 例：按用户名模糊查找  
{"PropertyName": "MIX", "Value": "666", "Operation":"5"}
{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="hasChild" type="boolean" required=true %}
是否包含下级 true:包含 false:不包含
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 1,
	"data": [{
		"ObjectID": 40247,
		"VehicleID": null,
		"HoldID": 11064,
		"MDTModel": 3126,
		"MDTModelName": "VDF-T0",
		"TrackerType": 0,
		"TrackerTypeName": "有线",
		"QueryPswd": null,
		"SIM": "1302001589",//SIM卡号
		"SIM2": "1302001589",// 设备ID
		"PayEndDate": "2019-05-25 17:46:50",
		"isVip": true,// 是否VIP
		"Remark": "",
		"InstallTime": null,
		"InstallPlace": null,
		"InstallPeopleID": 0,
		"CreateTime": "2016-01-30 14:47:01",
		"CreateUserID": null,
		"FullPathName": null,
		"StatusDes": "启动怠速[2分6秒],主电压13.9V,GSM强29,卫星中5,回传[13秒]",
		"isOnline": false,
		"Status": 0,
		"isAlarm": false,
		"RcvTime": "2017-11-15 18:38:07",// 接收时间
		"GPSTime": "2017-11-15 18:37:57",// GPS时间
		"Lon": 113.941995,
		"Lat": 22.556118,
		"OfflineDesc": ">1年",
		"VehicleName": "MT08_LED11",// 车牌
		"VehicleNumBackColor": "蓝色",
		"GPSFlag": 307,
		"Speed": 0,
		"TimeZone": 0.0,
		"Factory": "VDF",
		"ObjectType": 1
	}]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryDeviceDetail" %}
{% api-method-summary %}
QueryDeviceDetail
{% endapi-method-summary %}

{% api-method-description %}
查询设备详细信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="ObjectID" type="string" required=true %}
ObjectID
{% endapi-method-parameter %}

{% api-method-parameter name="language" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```text
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": {
		"device": {
			"ObjectID": 40247.0,
			"HoldID": 11064.0,
			"ObjectCode": null,
			"ObjectType": 1, // 车辆类型
			"VehicleNum": "MT08_LED11", // 车牌
			"QueryPwd": "123456", // 查询密码
			"Color": "",
			"MDTSerial": null,
			"SIM": "1302001589",//SIM卡号
			"SIM2": "1302001589",// 设备ID
			"AlldayContacter": "ZYW021",// 联系人
			"AlldayTel": "123457",// 电话
			"isDeleted": null,
			"MDTTypeID": 10.0,
			"EnterNetTime": null,
			"UpdateTime": "2019-04-11 10:56:01",
			"SeatNum": null,
			"MileAgeParam": null,
			"MileageOilParam": null,
			"CreateUser": 180,
			"CreateTime": "2016-01-30 14:47:01",
			"Modifier": 11174,
			"Remark": "",
			"ServiceEndDate": "2021-11-14 00:00:00",
			"MDTModel": 3126.0,// 设备型号
			"LedTypeID": 0,
			"MDTPwd": null,
			"VehicleNumBackColor": "蓝色", // 车牌颜色
			"AuthCode": null,
			"EMail": null,
			"TObjectID": null,
			"UserIDStr": null,
			"InstallPosition": "",
			"HomeAddress": "",
			"HomeLon": null,
			"HomeLat": null,
			"CompanyAddress": "",
			"CompanyLon": null,
			"CompanyLat": null,
			"PayEndDate": "2035-12-27 00:00:00",// 付费截止日期
			"TrackerType": 0,
			"VehicleID": 18591,
			"InstallTime": null,
			"InstallPeopleID": null,
			"PhotoName": "",
			"TimeZone": 0.0,
			"isVip": true,
			"ImgUrl": null
		},
		"holdInfo": {
			"HoldID": 11064,
			"Name": "001"
		},
		"modifyInfo": {
			"HoldID": 11174,
			"Name": "王岩"
		},
		"createInfo": {
			"HoldID": 180,
			"Name": "吴仕旭"
		},
		"carTypeList": [{
			"ItemID": 3,
			"DictID": 1,
			"ItemName": "大卡车",
			"ImgUrl": "/static/image/大卡车.gif",
			"Remark": "Van"
		}, {
			"ItemID": 10,
			"DictID": 1,
			"ItemName": "个人定位",
			"ImgUrl": "/static/image/个人定位.gif",
			"Remark": "Personal"
		}, {
			"ItemID": 15,
			"DictID": 1,
			"ItemName": "工程车",
			"ImgUrl": "/static/image/工程车.gif",
			"Remark": "car"
		}, {
			"ItemID": 6,
			"DictID": 1,
			"ItemName": "公交车",
			"ImgUrl": "/static/image/公交车.gif",
			"Remark": "car"
		}, {
			"ItemID": 16,
			"DictID": 1,
			"ItemName": "环卫车",
			"ImgUrl": "/static/image/环卫车.gif",
			"Remark": "car"
		}, {
			"ItemID": 8,
			"DictID": 1,
			"ItemName": "混凝土搅拌车",
			"ImgUrl": "/static/image/混凝土搅拌车.gif",
			"Remark": "EMV"
		}, {
			"ItemID": 9,
			"DictID": 1,
			"ItemName": "货车",
			"ImgUrl": "/static/image/货车.gif",
			"Remark": "Van"
		}, {
			"ItemID": 5,
			"DictID": 1,
			"ItemName": "警车",
			"ImgUrl": "/static/image/警车.gif",
			"Remark": "car"
		}, {
			"ItemID": 2,
			"DictID": 1,
			"ItemName": "救护车",
			"ImgUrl": "/static/image/救护车.gif",
			"Remark": "car"
		}, {
			"ItemID": 18,
			"DictID": 1,
			"ItemName": "旅游车",
			"ImgUrl": "/static/image/旅游车.gif",
			"Remark": "Others"
		}, {
			"ItemID": 12,
			"DictID": 1,
			"ItemName": "摩托车",
			"ImgUrl": "/static/image/摩托车.gif",
			"Remark": "Moto"
		}, {
			"ItemID": 11,
			"DictID": 1,
			"ItemName": "其他",
			"ImgUrl": "/static/image/其他.gif",
			"Remark": "Others"
		}, {
			"ItemID": 19,
			"DictID": 1,
			"ItemName": "挖机",
			"ImgUrl": "/static/image/挖机.gif",
			"Remark": "Excavator"
		}, {
			"ItemID": 7,
			"DictID": 1,
			"ItemName": "厢式车",
			"ImgUrl": "/static/image/厢式车.gif",
			"Remark": "car"
		}, {
			"ItemID": 1,
			"DictID": 1,
			"ItemName": "小轿车",
			"ImgUrl": "/static/image/小轿车.gif",
			"Remark": "car"
		}, {
			"ItemID": 4,
			"DictID": 1,
			"ItemName": "油罐车",
			"ImgUrl": "/static/image/油罐车.gif",
			"Remark": "car"
		}, {
			"ItemID": 17,
			"DictID": 1,
			"ItemName": "渣土车",
			"ImgUrl": "/static/image/渣土车.gif",
			"Remark": "car"
		}],
		"objectTypeList": [{
			"ItemID": 3130,
			"DictID": 58,
			"ItemName": "VDF-MT06",
			"Remark": "超长待机设备"
		}, {
			"ItemID": 3150,
			"DictID": 58,
			"ItemName": "VDF-LT01",
			"Remark": "有线设备9-100V,4G"
		}, {
			"ItemID": 3151,
			"DictID": 58,
			"ItemName": "VDF-LT03",
			"Remark": "可充电设备,4G"
		}, {
			"ItemID": 3161,
			"DictID": 58,
			"ItemName": "VDF-LT12",
			"Remark": "超长待机5年,4G集装箱设备"
		}, {
			"ItemID": 3162,
			"DictID": 58,
			"ItemName": "VDF-LT18",
			"Remark": "有线设备,TBox专用"
		}, {
			"ItemID": 3129,
			"DictID": 58,
			"ItemName": "VDF-MT01",
			"Remark": "全内置设备"
		}, {
			"ItemID": 3140,
			"DictID": 58,
			"ItemName": "VDF-MT01HC",
			"Remark": "有线CDMA设备9-100V,支持断油电"
		}, {
			"ItemID": 3139,
			"DictID": 58,
			"ItemName": "VDF-MT01HV",
			"Remark": "有线设备9-100V,支持断油电"
		}, {
			"ItemID": 3132,
			"DictID": 58,
			"ItemName": "VDF-MT02",
			"Remark": "长条形设备"
		}, {
			"ItemID": 3138,
			"DictID": 58,
			"ItemName": "VDF-MT02R",
			"Remark": "有线设备9-36V,支持长润的油位传感器"
		}, {
			"ItemID": 3137,
			"DictID": 58,
			"ItemName": "VDF-MT02S",
			"Remark": "有线设备9-100V,支持断油电"
		}, {
			"ItemID": 3133,
			"DictID": 58,
			"ItemName": "VDF-MT03",
			"Remark": "可充电设备"
		}, {
			"ItemID": 3131,
			"DictID": 58,
			"ItemName": "VDF-MT05",
			"Remark": "超长待机设备(MINI版)"
		}, {
			"ItemID": 3142,
			"DictID": 58,
			"ItemName": "VDF-MT06S",
			"Remark": "超长待机3年,带光感"
		}, {
			"ItemID": 3143,
			"DictID": 58,
			"ItemName": "VDF-MT06W",
			"Remark": "超长待3年，带WIFI"
		}, {
			"ItemID": 3135,
			"DictID": 58,
			"ItemName": "VDF-MT07",
			"Remark": "超长待机3年,带光感"
		}, {
			"ItemID": 3148,
			"DictID": 58,
			"ItemName": "VDF-MT07W",
			"Remark": "超长待机3年,带wifi"
		}, {
			"ItemID": 3136,
			"DictID": 58,
			"ItemName": "VDF-MT08",
			"Remark": "有线设备9-36V,预留两路串口可接附件"
		}, {
			"ItemID": 3146,
			"DictID": 58,
			"ItemName": "VDF-MT09",
			"Remark": "超长待机1年，单wifi"
		}, {
			"ItemID": 3149,
			"DictID": 58,
			"ItemName": "VDF-MT09S",
			"Remark": "长待机1年,带GPS&WIFI"
		}, {
			"ItemID": 3156,
			"DictID": 58,
			"ItemName": "VDF-MT12",
			"Remark": "3年长待机"
		}, {
			"ItemID": 3152,
			"DictID": 58,
			"ItemName": "VDF-NT01",
			"Remark": "有线设备9-100V,NB设备"
		}, {
			"ItemID": 3153,
			"DictID": 58,
			"ItemName": "VDF-NT02",
			"Remark": "有线设备9-100, NB设备"
		}, {
			"ItemID": 3158,
			"DictID": 58,
			"ItemName": "VDF-NT06",
			"Remark": "超长待机1年,GSM+NB+CAT-M"
		}, {
			"ItemID": 3154,
			"DictID": 58,
			"ItemName": "VDF-NT07",
			"Remark": "3年长待机,NB设备"
		}, {
			"ItemID": 3126,
			"DictID": 58,
			"ItemName": "VDF-T0",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3113,
			"DictID": 58,
			"ItemName": "VDF-T1",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3134,
			"DictID": 58,
			"ItemName": "VDF-T1S",
			"Remark": "T1升级版"
		}, {
			"ItemID": 3127,
			"DictID": 58,
			"ItemName": "VDF-T2",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3128,
			"DictID": 58,
			"ItemName": "VDF-T5",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3112,
			"DictID": 58,
			"ItemName": "VDF-T6",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3125,
			"DictID": 58,
			"ItemName": "VDF-T8",
			"Remark": "沃达孚"
		}, {
			"ItemID": 3160,
			"DictID": 58,
			"ItemName": "VDF-WT01",
			"Remark": "3G有线设备"
		}, {
			"ItemID": 3155,
			"DictID": 58,
			"ItemName": "VDF-WT08",
			"Remark": "3G版MT08 有线设备9-36V,预留两路串口可接附件"
		}, {
			"ItemID": 3157,
			"DictID": 58,
			"ItemName": "VDF-WT12",
			"Remark": "3G版MT12"
		}, {
			"ItemID": 3144,
			"DictID": 58,
			"ItemName": "VDF-WT26",
			"Remark": "3G超长待机3年"
		}, {
			"ItemID": 3159,
			"DictID": 58,
			"ItemName": "VDF-WT27",
			"Remark": "超长待机5年,3G设备"
		}, {
			"ItemID": 3145,
			"DictID": 58,
			"ItemName": "VDF-WT28",
			"Remark": "有线无线二合一，无线长待机3～5年"
		}, {
			"ItemID": 3123,
			"DictID": 58,
			"ItemName": "VDF-T",
			"Remark": "沃达孚JTT808部标终端"
		}, {
			"ItemID": 3141,
			"DictID": 58,
			"ItemName": "BSJ",
			"Remark": "博实结"
		}, {
			"ItemID": 3120,
			"DictID": 58,
			"ItemName": "GM-GT02",
			"Remark": "谷米GT02"
		}, {
			"ItemID": 3121,
			"DictID": 58,
			"ItemName": "GM-GT03",
			"Remark": "谷米GT03"
		}, {
			"ItemID": 3124,
			"DictID": 58,
			"ItemName": "GM-GT06",
			"Remark": "谷米GT06"
		}, {
			"ItemID": 3122,
			"DictID": 58,
			"ItemName": "GM-GW2318",
			"Remark": "谷米GW2318"
		}, {
			"ItemID": 3114,
			"DictID": 58,
			"ItemName": "HB-GDDB",
			"Remark": "华宝广东地标"
		}, {
			"ItemID": 3109,
			"DictID": 58,
			"ItemName": "HQ-V16S",
			"Remark": "华强"
		}, {
			"ItemID": 3105,
			"DictID": 58,
			"ItemName": "HQ-V36",
			"Remark": "华强"
		}, {
			"ItemID": 3106,
			"DictID": 58,
			"ItemName": "HQ-V52",
			"Remark": "华强"
		}, {
			"ItemID": 3107,
			"DictID": 58,
			"ItemName": "HQ-Y31",
			"Remark": "华强"
		}, {
			"ItemID": 3108,
			"DictID": 58,
			"ItemName": "HQ-Y51",
			"Remark": "华强"
		}, {
			"ItemID": 3119,
			"DictID": 58,
			"ItemName": "HYXT-518",
			"Remark": "鸿远信通"
		}, {
			"ItemID": 3102,
			"DictID": 58,
			"ItemName": "SG",
			"Remark": "赛格"
		}, {
			"ItemID": 3118,
			"DictID": 58,
			"ItemName": "TH-BG",
			"Remark": "天禾"
		}, {
			"ItemID": 3117,
			"DictID": 58,
			"ItemName": "TH-DG",
			"Remark": "天禾"
		}, {
			"ItemID": 3116,
			"DictID": 58,
			"ItemName": "TH-HQ",
			"Remark": "天禾"
		}, {
			"ItemID": 3115,
			"DictID": 58,
			"ItemName": "TH-TH",
			"Remark": "天禾"
		}, {
			"ItemID": 3147,
			"DictID": 58,
			"ItemName": "YIWEI-CL10",
			"Remark": "移为"
		}, {
			"ItemID": 3110,
			"DictID": 58,
			"ItemName": "YST-F1",
			"Remark": "赢时通"
		}, {
			"ItemID": 3111,
			"DictID": 58,
			"ItemName": "YST-F3",
			"Remark": "赢时通"
		}, {
			"ItemID": 3101,
			"DictID": 58,
			"ItemName": "YST-F7",
			"Remark": "赢时通"
		}, {
			"ItemID": 3103,
			"DictID": 58,
			"ItemName": "YST-F8",
			"Remark": "赢时通"
		}, {
			"ItemID": 3104,
			"DictID": 58,
			"ItemName": "YW-LJL",
			"Remark": "有为-蓝精灵"
		}]
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/ModifyDevice" %}
{% api-method-summary %}
ModifyDevice
{% endapi-method-summary %}

{% api-method-description %}
新增/修改 设备信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-type" type="string" required=true %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="newItem" type="string" required=true %}
设备信息  
传回从QueryDeviceDetail获得的信息，新增时QueryDeviceDetail接口的ObjectID传0
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/DeleteDevice" %}
{% api-method-summary %}
DeleteDevice
{% endapi-method-summary %}

{% api-method-description %}
删除设备信息
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="ObjectIDs" type="array" required=true %}
要删除的ID列表
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryHold" %}
{% api-method-summary %}
QueryHold
{% endapi-method-summary %}

{% api-method-description %}
查询 用户列表
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="pageIndex" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="pageSize" type="integer" required=true %}
页面数量
{% endapi-method-parameter %}

{% api-method-parameter name="sortKey" type="string" required=true %}
排序字段
{% endapi-method-parameter %}

{% api-method-parameter name="sortDirect" type="string" required=true %}
排序方向
{% endapi-method-parameter %}

{% api-method-parameter name="filters" type="array" required=true %}
查询条件
{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="hasChild" type="boolean" required=true %}
是否包含下级
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 1,
	"data": [{
		"HoldID": 10040,
		"HoldName": "沃达孚", // 用户名
		"Name": "沃达孚",
		"ParentHoldID": 17, // 上级用户ID
		"ParentHoldName": "0.研发测试", // 上级用户名
		"UserName": "66666666", // 登录账号
		"UserPassword": "666666",// 登录密码
		"Contacter": "沃达孚",// 联系人
		"Tel": "1", // 电话
		"MustTel": "1",
		"Fax": null,
		"Email": null,
		"Addr": null,
		"HoldType": null,
		"HoldTreePath": null,
		"CreateUser": null,
		"CreateTime": "2017-06-29 13:48:42", // 创建时间
		"Modifier": null,
		"FullPathName": "沃达孚",
		"Remark": "",
		"UserID": 0,
		"TimeZone": null,
		"ServiceEndDate": null,
		"ModifierName": null,
		"UpdateTime": null
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryHoldDetail" %}
{% api-method-summary %}
QueryHoldDetail
{% endapi-method-summary %}

{% api-method-description %}
查询用户详情
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="string" required=true %}
用户ID
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": {
		"hold": {
			"HoldID": 10040,
			"HoldName": "沃达孚",
			"Name": null,
			"ParentHoldID": 17,
			"ParentHoldName": "0.研发测试",
			"UserName": "6666666",
			"UserPassword": "123456",
			"Contacter": "沃达孚",
			"Tel": "1",
			"MustTel": null,
			"Fax": null,
			"Email": null,
			"Addr": "",
			"HoldType": null,
			"HoldTreePath": null,
			"CreateUser": null,
			"CreateTime": "2017-06-29 13:48:42",
			"Modifier": 11174,
			"FullPathName": "沃达孚",
			"Remark": "",
			"UserID": 11591,
			"TimeZone": null,
			"ServiceEndDate": "2019-05-31 00:00:00",
			"ModifierName": "wangyan",
			"UpdateTime": "2019-05-25 13:47:27"
		},
		"parentItem": {
			"Name": "0.研发测试",
			"HoldID": 17
		}
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/ModifyHold" %}
{% api-method-summary %}
ModifyHold
{% endapi-method-summary %}

{% api-method-description %}
新增/修改用户
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="newItem" type="object" required=true %}
新用户信息
{% endapi-method-parameter %}

{% api-method-parameter name="newFun" type="array" required=true %}
权限 传空数组
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/DeleteHold" %}
{% api-method-summary %}
DeleteHold
{% endapi-method-summary %}

{% api-method-description %}
删除用户
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="HoldIDs" type="string" required=true %}
用户ID数组
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryUser" %}
{% api-method-summary %}
QueryUser
{% endapi-method-summary %}

{% api-method-description %}
查询账号
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="pageIndex" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="pageSize" type="integer" required=true %}
页面数量
{% endapi-method-parameter %}

{% api-method-parameter name="sortKey" type="string" required=true %}
排序关键字
{% endapi-method-parameter %}

{% api-method-parameter name="sortDirect" type="string" required=true %}
排序方向
{% endapi-method-parameter %}

{% api-method-parameter name="filters" type="array" required=true %}
查询条件
{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="integer" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="hasChild" type="boolean" required=true %}
是否包含下级
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 1,
	"data": [{
		"UserID": 6666, // 账号ID
		"UserName": "6666",// 登录账号
		"UserPassword": "",// 登录密码
		"UserType": 952,
		"UserTypeName": "普通管理员",// 账号类型 
		"HoldID": 10040,//所属用户ID
		"UpdateTime": "2018-12-21 13:34:44",//更新时间
		"RealName": "dafu",// 真实姓名
		"StartTime": "2018-04-18 00:00:00",// 账号启动时间
		"EndTime": "2019-04-18 00:00:00",// 账号截止时间
		"HoldName": "沃达孚",// 用户名
		"FullPathName": "沃达孚",
		"Remark": ""
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/QueryUserDetail" %}
{% api-method-summary %}
QueryUserDetail
{% endapi-method-summary %}

{% api-method-description %}
查询账号详情
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="UserID" type="string" required=true %}
用户ID
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": {
		"user": {
			"UserID": 6666,
			"UserName": "666666",
			"UserPassword": "123456",
			"UserType": null,
			"HoldID": 666666,
			"ParentUserID": null,
			"UpdateTime": "2018-12-21 13:34:44",
			"isDeleted": null,
			"Remark": "",
			"RealName": "dafu",
			"StartTime": "2018-04-18 00:00:00",
			"EndTime": "2019-04-18 00:00:00",
			"DefaultFunID": null,
			"DefaultMapTypeID": null,
			"DefaultModel": null,
			"DefaultOverTimeDays": 0,
			"TUserID": null
		},
		"holdInfo": {
			"HoldID": 10040,
			"Name": "沃达孚"
		}
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/ModifyUser" %}
{% api-method-summary %}
ModifyUser
{% endapi-method-summary %}

{% api-method-description %}
修改账号
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="newItem" type="object" required=true %}
账号信息：QueryUserDetail获得的账号信息
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/Ver/2019/Appservice.asmx/DeleteUser" %}
{% api-method-summary %}
DeleteUser
{% endapi-method-summary %}

{% api-method-description %}
删除账号
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="UserIDs" type="string" required=true %}
账号ID数组
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/Appservice.asmx/AddMultiOrder" %}
{% api-method-summary %}
AddMultiOrder
{% endapi-method-summary %}

{% api-method-description %}
使用沃点升级VIP
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="ObjectIDs" type="array" required=true %}
设备ID列表
{% endapi-method-parameter %}

{% api-method-parameter name="PayYear" type="integer" required=true %}
升级年数
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="失败" %}
```javascript
{
	"errCode": 60001,
	"errMsg": "余额不足，请先充值",
	"total": null,
	"data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/Appservice.asmx/QueryWalletInfo" %}
{% api-method-summary %}
QueryWalletInfo
{% endapi-method-summary %}

{% api-method-description %}
获取钱包信息，升级价格
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="string" required=true %}
用户ID，可为null，默认为登录用户
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": null,
	"data": {
		"Name": "003",     // 用户名
		"TotalBalance": 0, // 余额
		"isSelf": true,    // 是否用户自身
		"key_price": 12,   // 有线设备升级VIP年价
		"key_price2": 6    // 无线设备升级VIP年价
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/AppService.asmx/QueryWalletList" %}
{% api-method-summary %}
QueryWalletList
{% endapi-method-summary %}

{% api-method-description %}
查询消费明细
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="pageIndex" type="integer" required=true %}
页码
{% endapi-method-parameter %}

{% api-method-parameter name="pageSize" type="integer" required=true %}
页面数量
{% endapi-method-parameter %}

{% api-method-parameter name="sortKey" type="string" required=true %}
排序字段，可为空字符串
{% endapi-method-parameter %}

{% api-method-parameter name="sortDirect" type="string" required=true %}
排序关键字，可为空字符串
{% endapi-method-parameter %}

{% api-method-parameter name="filters" type="array" required=true %}
过滤数组，可为空数组
{% endapi-method-parameter %}

{% api-method-parameter name="HoldID" type="integer" required=true %}
用户ID，可为null，默认为登录用户
{% endapi-method-parameter %}

{% api-method-parameter name="hasChild" type="boolean" required=true %}
是否包含下级
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
	"errCode": 0,
	"errMsg": "ok.",
	"total": 713, // 总行数
	"data": [{
		"MID": 12386, // 记录ID
		"OrderNO": "20190321DQ8IMBGSK0", // 订单号
		"HoldID": 17, // 消费用户ID
		"HoldName": "0.研发测试", // 用户名
		"FullPath": "GPS管理中心->0.研发测试", // 全路径
		"OccurName": "车辆续期", // 服务名称
		"OccurMoney": -5.00, // 花费沃点
		"OccurTime": "2019-03-21 10:27:23", // 创建时间
		"RemainMoney": 4075.00, // 剩余沃点
		"Remark": "123", // 备注
		"CreateUserID": 0, // 创建用户ID
		"CreateUserName": null // 创建用户名
	}, {
		"MID": 12385,
		"OrderNO": "20190321IU9MBC3N4U",
		"HoldID": 17,
		"HoldName": "0.研发测试",
		"FullPath": "GPS管理中心->0.研发测试",
		"OccurName": "车辆续期",
		"OccurMoney": -5.00,
		"OccurTime": "2019-03-21 10:22:12",
		"RemainMoney": 4080.00,
		"Remark": "123",
		"CreateUserID": 0,
		"CreateUserName": null
	}]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/AppService.asmx/CreateAlipayOrder" %}
{% api-method-summary %}
CreateAlipayOrder
{% endapi-method-summary %}

{% api-method-description %}
创建支付宝订单
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="totalPoints" type="integer" required=true %}
充值沃点数量
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
    "errCode": 0,
    "errMsg": "ok.",
    "total": null,
    "data": {
        "app_id": "2016092600599323",
        "method": "alipay.trade.app.pay",
        "format": "json",
        "charset": "utf-8",
        "sign_type": "RSA2",
        "sign": "DTNVJsU9Jpo+sN2WB7VJ4ZRHW4ID7487DnkbipVLaiUEhyTqfZW9y7fx0CP0DbOj2PROY/XWsAelrc4oBZAbQi80zQhMAGMJ8etvbeps+QFejgoUlMM0bGnCl9bnrKOd95XwA5MQon5d9jvyvxTU1ubupBqorxseFzC2K5EDADI8W0y6qQeRhKsIShUeXqmn8GKfIAg9HVpisapS/ZZ3GTpzdhGk/uDr7MGQTCZP7434yawiDjLMq80l53L9pLimsjgrbbg7d3fRPAn4zN4qUDSHI5p9y4ZexwQ/QjiqavZamHCc5hNoG4WX5ae1SouydViLleGQmI8m0+w4Hgoe0A==",
        "timestamp": "2019-03-25 16:23:43",
        "version": "1.0",
        "notify_url": "http://d4ec0697.ngrok.io/api/pay/notifyalipay.aspx",
        "biz_content": "{\"body\":\"沃点充值 + 50\",\"subject\":\"沃点充值 + 50\",\"out_trade_no\":\"20190325KD74IBTXHC\",\"timeout_express\":\"15m\",\"total_amount\":\"50\",\"product_code\":\"QUICK_MSECURITY_PAY\",\"goods_type\":\"0\"}"
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="失败" %}
```javascript
{
    "errCode": 50062,
    "errMsg": "充值数量不能小于1",
    "total": null,
    "data": null
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://127.0.0.1" path="/Ver/2019/AppService.asmx/IsWxPaySuccess" %}
{% api-method-summary %}
IsWxPaySuccess
{% endapi-method-summary %}

{% api-method-description %}
查询订单是否支付完成
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="loginKey" type="string" required=true %}
登录凭证
{% endapi-method-parameter %}

{% api-method-parameter name="orderNo" type="string" required=true %}
订单号
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```javascript
{
    "errCode": 0,
    "errMsg": "ok.",
    "total": null,
    "data": {
        "isSuccess": false
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="" path="/api/posts/posts.ashx" %}
{% api-method-summary %}
posts.ashx
{% endapi-method-summary %}

{% api-method-description %}
图像上传接口，上传成功后返回文件名
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="userId" type="string" required=true %}
用户ID
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=true %}
图片类型:"image"
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=false %}
multipart/form-data
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="file" type="object" required=true %}
上传的图片,type:file
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="成功" %}
```
20190524095049_11993_vF6jU_1 (12).jpg
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

