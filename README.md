# igps接口文档

{% api-method method="post" host="https://192.168.0.75/igps" path="/AppService.asmx/Login" %}
{% api-method-summary %}
Login
{% endapi-method-summary %}

{% api-method-description %}
登录接口
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-form-data-parameters %}
{% api-method-parameter name="OSType" type="integer" required=true %}
手机系统类型 0: 安卓 1: IOS 2: WP 3:WX
{% endapi-method-parameter %}

{% api-method-parameter name="UserPswd" type="string" required=true %}
登录密码/查询密码
{% endapi-method-parameter %}

{% api-method-parameter name="UserName" type="string" required=true %}
登录账号/登录车牌
{% endapi-method-parameter %}

{% api-method-parameter name="LoginType" type="integer" required=true %}
登录账户类型  0: 用户登录  1: 车牌登录
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="1.登录成功" %}
```javascript
{
    "Data": {
        "Status": "1",
        "Type": "0",
        "Msg": "0.研发测试",
        "ObjectID": "17",
        "SF": "0",
        "LoginKey": "A8203EFF616B54DF0CD1CB5E208C0225"
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="2.登录失败" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<string xmlns="http://www.vodofo.com/">{"Data":{"Status":"0","Msg":"登录信息有误","LoginKey":""}}</string>
```
{% endcode-tabs-item %}

{% code-tabs-item title="3.账号为空" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<string xmlns="http://www.vodofo.com/">{"Data":{"Status":"0","Msg":"","LoginKey":""}}</string>
```
{% endcode-tabs-item %}

{% code-tabs-item title="4.车牌登录" %}
```markup
<?xml version="1.0" encoding="utf-8"?>
<string xmlns="http://www.vodofo.com/">{"Data":{"Status":"1","Type":"1","Msg":"谷德80222001632","ObjectID":"133018","SF":"0","LoginKey":"B267747AF42223B50F6BB7B7934F4F80"}}</string>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

返回参数说明

| 参数名 | 是否必须 | 说明 |
| :--- | :--- | :--- |
| Data | 是 |  |
|  | 是 | 1：登录成功，0：失败 |
| Type | 否 | 0：用户登录，1：车牌登录 |
| Msg | 否 | 用户名称/车牌 |
| ObjectID | 否 | 用户ID/车辆ID |
| LoginKey | 否 |  |



