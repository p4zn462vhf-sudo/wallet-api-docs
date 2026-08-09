For the complete documentation index, see llms.txt. This page is also available as Markdown.
复制
获取钱包提币地址 (wap.address)

应用场景：商户系统向平台发起获取H5钱包提币地址请求，平台返回对应钱包H5提币地址。

请求报文(业务参数定义)

节点名

字段名称

可空

类型

备注

merchUid

商户UID

必填

N

商户UID

userNo

用户编号

必填

C (1,20)

发起请求的用户唯一标识

userName

用户真实姓名

必填

C (1,32)

发起请求的用户真实姓名

currency

交易币种（代币）

必填

C (1,16)

参考交易币种字典

请求报文示例

{

       "data":"{\"merchUid\":\"42400\",\"userNo\":\"9527\",\"userName\":\"张三\",\"currency\":\"CNY\"}",

       "cusUid": "42400",

       "transCode": "wap.address",

"signMsg":"w4RnasO0wQjwk2g5duZbIPoDZU3RGdhat0Xv3giimOgI8uIQlZDMbjkO2zCCL8qOmUuD+mcntZUkJzztSkaGM/fP3QHaplIWn41QIJ7aDZ5atOMDO4R10xD7HpTPkXgP8xLoeq9HHmRCxIcGEdFmrGUMDqglbtii7MjglQo+mpaIFKKwDEOzNwan4xNdM7s74Z7XITRT/PIEfDCNguy92xERc24aafA26QATi1rJkAFXASI7h9wrHb9EYFLNNwbyi/YLGllwSV8U8+v+XJ+BS0Sx6pSxJx3C+ESYSFhlaE/oT5/QHppRntl1+py510yGji3YvDgpGON6zKjOxbnb9Q==",

       "version": "01",

       "reqSn": "424001698774299034"

}

响应报文(业务参数定义)

节点名

字段名称

可空

类型

备注

merchUid

商户UID

必填

N

商户UID

userNo

用户编号

必填

C (1,20)

发起请求的用户唯一标识

userName

用户真实姓名

必填

C (1,32)

发起请求的用户真实姓名

recAddress

APP提币地址

必填

C (1,32)

提币地址

userUid

用户UID

必填

N

用户UID

注:  解析说明
1、retCode 为000000，代表获取钱包提币地址成功

2、retCode 为其它情况，代表获取钱包提币地址失败

响应报文示例

{

       "cusUid": "42400",

"data":"{\"merchUid\":42400,\"userNo\":\"9527\",\"userName\":\"张三\",\"recAddress\":\"424001000372XCDDFFF80559CDBC51\",\"currency\":\"CNY\",\"userUid\":\"9527111\",}",

       "reqSn": "424001698774299034",

       "retCode": "000000",

       "retMsg": "请求成功",

"signMsg":"eswFdIg4etv6B+yRLMk7NgAx+ncmANu/2LL1rXEfbWd4Qd3mFU4FzOch3+6FntenJJoJfzJ7iPS/SzjzvPakT+7GxmTGCvto9SlZ8vpt40cN6Dfck4M1Bae1OU/AG8x0uPyT8Mq5ue12hqKaP6dlJJwsQkQUopN1HVHgVHEkYmQAuBEjPoQRrNzUbsNf0E4sVXa1I9GcM2+ayq6PFY57PwVNVoC4P7vViKKJgXG+oC05+5NTO93Ias6STn+4Au++LdkFGrlD/t2bQptqiCqPDaQyEjVHqybkpaBYHo7l16tX7Zj4D2eKdl6Qd4GE+gWewaSSxmKcW/+gQ7Nt7haq4A==",

       "transCode": "wap.address",

       "version": "01"

}

上一页
获取进入钱包链接 (wap.login)
下一页
商户扫码充币下单(scan.deposits.request)

最后更新于 2个月前