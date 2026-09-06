# 获取进入钱包链接 (wap.login)

**应用场景**：商户系统向平台发起获取进入钱包链接请求，返回对应进入钱包链接。

***

### 1. 请求报文

#### 业务参数定义

| 节点名             | 字段名称     | 可空  | 类型       | 备注                                                                                     |
| --------------- | -------- | --- | -------- | -------------------------------------------------------------------------------------- |
| `merchUid`      | 商户UID    | 必填  | N        | 商户UID                                                                                  |
| `currency`      | 交易币种(法币) | 必填  | C (1,16) | 参考交易币种字典(法币)                                                                           |
| `userNo`        | 用户编号     | 必填  | C (1,32) | 发起支付的用户唯一标识                                                                            |
| `userName`      | 用户真实姓名   | 必填  | C (1,32) | 用户付款账户的真实姓名                                                                            |
| `userIp`        | 用户IP地址   | 必填  | C (1,64) | 用户发起支付时的IP地址                                                                           |
| `userLevel`     | 用户等级     | 非必填 | N        | 用户等级,如：0、1、2、3、4、5、6、7、8、9等级                                                           |
| `merchInfo`     | 商户平台信息   | 必填  | C (1,30) | 用于在钱包充币页面展示商户平台                                                                        |
| `acctNoHistory` | 历史账号后缀   | 可空  | C (4,50) | 历史账号后缀(后4位)，多个后缀以英文逗号拼接，例如：1111,2222,3333                                              |
| `expectedAmt`   | 期望下单金额   | 可空  | C (0,13) | 期望下单金额，为String，可以为单个金额或金额区间（金额区间以-拼接，小金额在前，大金额在后），金额范围：1-999999；H5购买页面将优先展示符合期望下单金额的广告 |

#### 请求报文示例

```json
{
  "data": "{\"merchUid\":\"42400\",\"currency\":\"CNY\",\"userNo\":\"9527\",\"userName\":\"张三\",\"userIp\":\"用户真实IP地址\",\"userLevel\":\"0\",\"merchInfo\":\"XXX商户\",\"acctNoHistory\":\"1111,2222,3333\"}",
  "cusUid": "42400",
  "transCode": "wap.login",
  "signMsg": "w4RnasO0wQjwk2g5duZbIPoDZU3RGdhat0Xv3giimOgI8uIQlZDMbjkO2zCCL8qOmUuD+mcntZUkJzztSkaGM/fP3QHaplIWn41QIJ7aDZ5atOMDO4R10xD7HpTPkXgP8xLoeq9HHmRCxIcGEdFmrGUMDqglbtii7MjglQo+mpaIFKKwDEOzNwan4xNdM7s74Z7XITRT/PIEfDCNguy92xERc24aafA26QATi1rJkAFXASI7h9wrHb9EYFLNNwbyi/YLGllwSV8U8+v+XJ+BS0Sx6pSxJx3C+ESYSFhlaE/oT5/QHppRntl1+py510yGji3YvDgpGON6zKjOxbnb9Q==",
  "version": "01",
  "reqSn": "424001698774299034"
}
```

***

### 2. 响应报文

#### 业务参数定义

| 节点名        | 字段名称   | 可空 | 类型        | 备注          |
| ---------- | ------ | -- | --------- | ----------- |
| `merchUid` | 商户UID  | 必填 | N         | 商户UID       |
| `userNo`   | 用户编号   | 必填 | C (1,32)  | 发起支付的用户唯一标识 |
| `userName` | 用户真实姓名 | 必填 | C (1,32)  | 用户付款账户的真实姓名 |
| `userUid`  | 用户UID  | 必填 | N         | 用户UID       |
| `url`      | 进入钱包链接 | 必填 | C (1,128) | 进入钱包链接      |

> **解析说明**：
>
> 1. `retCode` 为 `000000`，代表获取进入钱包链接成功。
> 2. `retCode` 为其它情况，代表获取进入钱包链接失败。

#### 响应报文示例

```json
{
  "cusUid": "42400",
  "data": "{\"merchUid\":42400,\"userName\":\"张三\",\"userNo\":\"9527\",\"userUid\":1004157,\"url\":\"[http://127.0.0.1:8080/index?data=66E36921213666685DFE68CDE7D9CF026F6579966391C07F9A9FBEC7FD88D9BB7486D9D49011EBD6D2C19F6A16E247C3D128B3828C67A497B49E612EA89DB7999E54CEBFFA222382C455DD5C320E931D0F41FC10C0904146FE910542BF98C25477CE65CFFFE02B170E50ACF4BB541EA56DA5B78D7860C8B453D15983CBDDCD4F780C2B98FFD134BCAB79DB84B5F7734DB59D925B43C657A6A8FB51CD1293834C11DC077C797F744AB7F34CA5BB2DE078812CACDEC4CB39413ACD3A5C668C3670](http://127.0.0.1:8080/index?data=66E36921213666685DFE68CDE7D9CF026F6579966391C07F9A9FBEC7FD88D9BB7486D9D49011EBD6D2C19F6A16E247C3D128B3828C67A497B49E612EA89DB7999E54CEBFFA222382C455DD5C320E931D0F41FC10C0904146FE910542BF98C25477CE65CFFFE02B170E50ACF4BB541EA56DA5B78D7860C8B453D15983CBDDCD4F780C2B98FFD134BCAB79DB84B5F7734DB59D925B43C657A6A8FB51CD1293834C11DC077C797F744AB7F34CA5BB2DE078812CACDEC4CB39413ACD3A5C668C3670)\"}",
  "reqSn": "424001698774299034",
  "retCode": "000000",
  "retMsg": "请求成功",
  "signMsg": "eswFdIg4etv6B+yRLMk7NgAx+ncmANu/2LL1rXEfbWd4Qd3mFU4FzOch3+6FntenJJoJfzJ7iPS/SzjzvPakT+7GxmTGCvto9SlZ8vpt40cN6Dfck4M1Bae1OU/AG8x0uPyT8Mq5ue12hqKaP6dlJJwsQkQUopN1HVHgVHEkYmQAuBEjPoQRrNzUbsNf0E4sVXa1I9GcM2+ayq6PFY57PwVNVoC4P7vViKKJgXG+oC05+5NTO93Ias6STn+4Au++LdkFGrlD/t2bQptqiCqPDaQyEjVHqybkpaBYHo7l16tX7Zj4D2eKdl6Qd4GE+gWewaSSxmKcW/+gQ7Nt7haq4A==",
  "transCode": "wap.login",
  "version": "01"
}
```
