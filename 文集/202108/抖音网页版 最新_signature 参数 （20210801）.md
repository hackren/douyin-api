
# 抖音网页版 最新_signature 参数 （20210801）

抖音最近出了网页版，几乎福利：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/97322/1628383076012-6ca4a5d8-819c-43a6-a79d-e02324faf48b.png#clientId=u7f010c5f-e757-4&from=paste&height=812&id=u45388973&name=image.png&originHeight=1624&originWidth=2498&originalType=binary&ratio=1&size=4558916&status=done&style=none&taskId=udb0160e8-43d7-49fe-934d-3f78cfaf4c2&width=1249)




---



数据采集接口请求参数和返回数据更多信息请[点击查看接口文档](https://docs.qq.com/doc/DU3RKUFVFdVhQbXlR)

---

​

研究了下：发现几个api只有_signature参数加密

## 抖音用户视频列表接口分析

## 1、从抖音 APP 分享个人信息，复制链接，获得个人主页地址，示例：
​


## 2、使用 Chrome 抓包，获取视频列表接口的请求信息
​


#### 接口请求详情
​

参数分析：
​

user_id: 用户ID，可从 HTML 中提取
sec_uid: 空
count: 视频数量
max_cursor: 视频索引位置，用于翻页
aid: 固定值 1128
_signature: 实时签名值，由签名算法计算
dytk: 用户 token，可从 HTML 中提取
​


## 3、定位 _signature 签名算法
​

定位 __M
​


## 4、分析签名算法的执行逻辑
​

① 定义 __M 对象，及其 define 和 require 函数
​

② 执行 __M.define("douyin_falcon:node_modules/byted-acrawler/dist/runtime......" 这段代码
​

③ 执行 _bytedAcrawler = require("douyin_falcon:node_modules/byted-acrawler/dist/runtime")
​

④ 计算签名值 _signature = _bytedAcrawler.sign(user_id)
​

使用 NodeJS 提供签名计算服务
​

此处可能存在跨语言频繁调用的场景，所以使用 grpc 提供服务。
​

​

