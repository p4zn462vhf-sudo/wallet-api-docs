# 商户充币下单--深度集成(deposits.request)

**应用场景**：钱包用户在商户系统创建的充币订单，向平台发起商户充币下单请求，平台受理下单返回确认充币链接，该接口适用于进行深度集成的商户。

***

### 1. 请求报文

#### 业务参数定义

| 节点名             | 字段名称     | 可空  | 类型        | 备注                              |
| --------------- | -------- | --- | --------- | ------------------------------- |
| `merchUid`      | 商户UID    | 必填  | N         | 商户UID                           |
| `merchOrderNo`  | 商户单号     | 必填  | C (1,64)  | 商户系统唯一订单号                       |
| `currency`      | 交易币种（代币） | 必填  | C (1,16)  | 参考交易币种字典                        |
| `orderAmt`      | 下单数量     | 必填  | N         | 下单数量                            |
| `userNo`        | 用户编号     | 必填  | C (1,32)  | 发起支付的用户唯一标识                     |
| `userIp`        | 用户IP地址   | 必填  | C (1,64)  | 用户发起支付时的IP地址                    |
| `userName`      | 用户真实姓名   | 必填  | C (1,32)  | 用户付款账户的真实姓名                     |
| `userLevel`     | 用户等级     | 非必填 | N         | 用户等级，如：0、1、2、3、4、5、6、7、8、9等级    |
| `merchInfo`     | 商户平台信息   | 可空  | C (1,30)  | 用于在钱包充币页面展示商户平台                 |
| `notifyUrl`     | 交易结果通知地址 | 必填  | C (1,128) | 交易结果终态时根据该地址通知商户系统              |
| `extrasContent` | 扩展内容     | 可空  | C (0,256) | 预留扩展对象，没有则不传，扩展内容序列化后总长度不可超过256 |

#### 请求报文示例

```json
{
  "data": "{\"merchUid\":48351,\"merchInfo\":\"商户信息\",\"userLevel\":99,\"userNo\":\"1120\",\"extrasContent\":\"{\\\"a\\\":1111,\\\"b\\\":2222}\",\"merchOrderNo\":\"4813805310\",\"userIp\":\"127.0.0.1\",\"notifyUrl\":\"[http://127.0.0.1](http://127.0.0.1)\",\"currency\":\"TTT\",\"orderAmt\":54.47,\"userName\":\"1120\"}",
  "cusUid": "48351",
  "transCode": "deposits.request",
  "signMsg": "HauzduENQiV7WVotNpGTGjrGN3m4bx/oYDFgXpTvEqYY4IfgTs4LgulvyeqPHG2ccEGyJFZKSZ80TbupfWSfQ/5NasQ+BhEAlGgf4SiYCepxSuFqiU60Dz7bpSTPtFB3STe/iQNogsV0alsfGpPUtCCSPuRun9plB5bk8MZgm0g+c1iXOcdEH6xd4A+yo4VkkFrGnVz3P1zfmg8XPQCsuOVQgz1VbcHVHdjEoh+jal8/Be6ZXQcH6QLSKbgLZKZ76wV9CQ/FNIsYlqRWujRfGQqL2WpVdoPqrFznyr3ERlEdhLUkV6HrWquyoR/dW50L5FWTcKDnVGhMj5OduGaq7A==",
  "version": "01",
  "reqSn": "483511700644932447"
}
```

***

### 2. 响应报文

#### 业务参数定义

| 节点名             | 字段名称   | 可空 | 类型        | 备注                              |
| --------------- | ------ | -- | --------- | ------------------------------- |
| `merchUid`      | 商户UID  | 必填 | N         | 商户UID                           |
| `merchOrderNo`  | 商户单号   | 必填 | C(1,64)   | 商户系统唯一订单号                       |
| `userNo`        | 用户编号   | 必填 | C (1,32)  | 发起支付的用户唯一标识                     |
| `userName`      | 用户真实姓名 | 必填 | C (1,32)  | 用户付款账户的真实姓名                     |
| `userUid`       | 用户UID  | 必填 | N         | 用户UID                           |
| `orderNo`       | 平台单号   | 必填 | C(19)     | 平台唯一订单号                         |
| `tradeDate`     | 交易日期   | 必填 | C(8)      | 平台下单日期，格式:yyyyMMdd              |
| `orderAmt`      | 下单数量   | 必填 | N         | 下单数量                            |
| `status`        | 下单状态   | 必填 | N         | 10:下单成功                         |
| `url`           | 确认充币链接 | 必填 | C(1,1024) | 确认充币链接                          |
| `remark`        | 业务返回描述 | 必填 | C(1,64)   | 业务返回描述                          |
| `extrasContent` | 扩展内容   | 可空 | C (0,256) | 预留扩展对象，没有则不传，扩展内容序列化后总长度不可超过256 |

> **解析说明**：
>
> 1. `retCode` 为 `000000`，并且 `data` 中的 `status` 为 `10`，代表商户充币下单受理成功(不代表交易成功)。
> 2. `retCode` 为其它情况，代表商户充币下单失败。

#### 响应报文示例

```json
{
  "transCode": "deposits.request",
  "version": "01",
  "cusUid": "48351",
  "reqSn": "483511700644932447",
  "retCode": "000000",
  "retMsg": "请求成功",
  "data": "{\"extrasContent\":\"{\\\"a\\\":1111,\\\"b\\\":2222}\",\"merchOrderNo\":\"4813805310\",\"merchUid\":48351,\"orderAmt\":54.47,\"orderNo\":\"2023112217221290370\",\"remark\":\"请求成功\",\"status\":10,\"tradeDate\":\"20231122\",\"url\":\"[http://127.0.0.1:19014/index?data=75607770E373551EA164B331784C7B49F154779C8AF5464DF1063072DED59BF25B7C3BB94776800FBA1ED7548631FC733F130BCCB37A86EFCFD5EE279E52B3A11D8C8F8E15B48916C104DEE25BB1F4BDBBA451EE7FAD51AEA29FD36378D300972FECC75B0A73F664F07BC6A0107014FBF08E4DBE51547512BC1ACE031D6B6189B3601DD2EBD73D522C8A71BEC695C97F5C637433D2F906713EBD40F708300D966B6DDF8DB826B9BD1256F5AEBD8582E8E6F36070AC9F0A09645F48F89E07E384E46CBB9A52815B945978AB1EEABBC936DED0552749196B3D40B9C61DCB45A6C1B3288F2C357127769BB91B483F96D195](http://127.0.0.1:19014/index?data=75607770E373551EA164B331784C7B49F154779C8AF5464DF1063072DED59BF25B7C3BB94776800FBA1ED7548631FC733F130BCCB37A86EFCFD5EE279E52B3A11D8C8F8E15B48916C104DEE25BB1F4BDBBA451EE7FAD51AEA29FD36378D300972FECC75B0A73F664F07BC6A0107014FBF08E4DBE51547512BC1ACE031D6B6189B3601DD2EBD73D522C8A71BEC695C97F5C637433D2F906713EBD40F708300D966B6DDF8DB826B9BD1256F5AEBD8582E8E6F36070AC9F0A09645F48F89E07E384E46CBB9A52815B945978AB1EEABBC936DED0552749196B3D40B9C61DCB45A6C1B3288F2C357127769BB91B483F96D195)\",\"userName\":\"1120\",\"userNo\":\"1120\",\"userUid\":1004337}",
  "signMsg": "cGCKUj3/iwUoxP/lN+/M+jsWyF2CwhSMk/LmyRX8VlhFJbIRV/6+UctLb9gEtCa4BQPQMyLIsgXL/5LjEdbMpq1ZL6Wr2KnYsIzgxYfpjZPqXi+g2ySxOo+pG/K0CxBK/CNoxSM+IbWwDPCzgM+8NWe09qg6fNc3GBpcGgt9kGQx2Xs3dc9BKrIJ8Cy0lU8ossu7Xt6G5NYKjL1AnYsFdGBt6a1DBrX8oEp8i93ntFeKsdakiLf04TbRj5QUwHsJ+uIGJENidY+rwJ8VsuzUhIMULupqMi3ffsFR/W9XkoSO95V7YhPq1JjGfOKaHu/+ZN922q8XGv+ReMcjT2JxgA=="
}
```
