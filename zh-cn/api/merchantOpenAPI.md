# 概述

## 1.请求域名

收钱吧接入域名(api_domain)：https://api-vendor.shouqianba.com

测试环境域名：https://api-sandbox.test.shouqianba.com

## 2.需要参与签名的接口及参数

   需要使用服务商序列号(vendor_sn)和服务商密钥(vendor_key)进行签名的接口：
  
-   [商户入网接口     /v2/merchant/create](https://doc.shouqianba.com/zh-cn/api/interface/merchantCreate.html)
   
-   [商户信息接口     /v2/merchant/info](https://doc.shouqianba.com/zh-cn/api/interface/merchantInfo.html)
   
-   [商户禁用接口     /v2/merchant/close](https://doc.shouqianba.com/zh-cn/api/interface/merchantClose.html)
   
-   [开户银行接口     /v2/merchant/banks](https://doc.shouqianba.com/zh-cn/api/interface/merchantBanks.html)
   
-   [支行列表接口     /v2/merchant/branches](https://doc.shouqianba.com/zh-cn/api/interface/merchantBranches.html)

-   [上传图片接口     /v2/merchant/upload](https://doc.shouqianba.com/zh-cn/api/interface/merchantUpload.html)
   
## 3.签名方法

如果要正常使用各接口，需要按照以下方式去进行签名验证:
 * 支付平台所有的API仅支持JSON格式的请求调用，请务必在HTTP请求头中加入Content-Type: application/json。
 * 所有请求的body都需采用UTF-8编码，所有响应也会采用相同编码。
 * 支付平台所有的API调用都需要签名验证。
 * 采用应用层签名机制。将HTTP请求body部分的UTF-8编码字节流视为被签名的内容，不关心主体的格式。
 * 签名人序列号(sn)和签名值(sign)放在HTTP请求头中，在接入服务中统一校验。
 * 签名算法: sign = MD5( CONCAT( body + key ) )
 * 签名首部: Authorization: sn + " " + sign
 * 所有返回参数都为 JSON 格式，请务必在HTTP请求头中加入Content-Type: application/json。
 * 所有请求的body都需采用UTF-8编码，所有响应也会采用相同编码。
 * 所有返回数据的类型都是 字符串。

## 4.通讯响应码说明及通讯错误码列表

   [见附录](https://doc.shouqianba.com/zh-cn/api/annex/responseCode.html)