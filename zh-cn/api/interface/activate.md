# 激活
激活接口用于获取交易接口签名需要的参数（终端号和终端密钥）。激活接口需要使用服务商的密钥签名。签名方法参考[签名机制文档](https://wosai.gitbooks.io/shouqianba-doc/content/zh-cn/api/sign.html)。

	请使用服务商序列号（vendor_sn）作为签名人序列号，服务商密钥（vendor_key）作为签名密钥。
## 接口名
{api_domain}/terminal/activate
## 请求类型
application/json
### 请求参数
字段名 | 类型 | 是否必填 | 说明
------ | ----- | -----| -----
app_id | string | Y | app id，从服务商平台获取
code | string | Y | 激活码内容
device_id | string(128) | Y | 设备唯一身份ID
client_sn | string(50) | N | 第三方终端号，必须保证在app id下唯一
name | string(128) | N | 终端名
os_info | string(45) | N |当前系统信息，如: Android5.0
sdk_version | string(45) | N | SDK版本

### 响应
字段名 | 类型 | 是否必填 | 说明
------ | ----- | -----| -----
terminal_sn | string | Y | 终端号
terminal_key | string | Y | 终端密钥

返回的状态请参考<font color="red">**附录**</font>

如：

```json
{
  "result_code": "200",
  "biz_response": {
    "terminal_sn": "10298371039",
    "terminal_key": "68d499beda5f72116592f5c527465656"
  }
}
```
##激活接口接入常见问题

###1.什么是收钱吧终端？
指实际进行交易的媒介系统，可以为实体收银机系统、智能设备里的APP、线上网页（e.g. 线上购物、会员充值等）
每个门店下都允许存在多个终端。

###2.device_id是什么？
设备指纹device_id唯一标识一台设备的编号，如Android设备的IMEI，IOS设备的identifierForVendor。


###1.激活时报签名错误
    1)请检查一下激活接口传入的参数是否有问题
    2)http请求是否正确签名。
    
###2.激活时报激活码过期
    一个激活码目前的有效期是7天，7天没有激活，就需要重新申请激活码

###3.激活时报激活码已经被使用
   每个激活码都有使用次数，激活次数用完就不能再使用了，需要重新申请新的激活码。
   
###4.激活时报设备号重复
   如果在同一个商户下终端的设备号已经被使用过了，就不能再次去使用那个终端号去激活，需要更换终端号，或者联系商务解绑之前激活的终端，才能再次激活。
   
###5.激活码是否可作为固定的参数存储起来？
不可以!激活码是与门店相对应的，每一个激活码都有可激活次数限制。将激活码作为固定参数存储很容易发生激活码失效等问题。
另外，共用激活码不便于商户日后在[商户系统](http://s.shouqianba.com/#/order)中对账。

###6.激活码是不是每一台终端都需要一个？
激活码是与门店相对应的，目前建议商户为每个终端单独生成一个激活码。
同时收钱吧也支持同一门店多终端共用一个激活码。此时，同一个激活码每次调用激活接口，返回的终端号和终端密钥是不一样的。

###7.激活接口的作用
收钱吧所有交易都需要终端号和终端密钥。
激活终端是为了拿到交易接口签名需要的参数（终端号和终端密钥），激活完一台终端，开发者需要把终端号和终端密钥信息持久化保持，以后每日签到更新终端密钥。
不管是支付（B扫C）还是预下单（C扫B）以及wap支付都需要激活后才能调用。
        一个终端只需激活一次，之后调用支付类接口（不论支付还是预下单）都不需要再激活。
	不需要每次进入程序时都调用激活函数。
	收钱吧不对同一个终端的激活次数做限制，开发者需要自行判断终端是否已激活。
	服务商参数vendor_sn和vendor_key是不变的，建议写死在程序里，以后直接输入激活码激活终端。
   
