# 解析抖音直播protocbuf弹幕数据

在开始分析之前需要准备好:<br>1.protobuf安装，composer安装protoc支持库<br>2.直播间弹幕抓包;<br>3.解析protoc protoc --decode_raw < xxx.bin 查看解析后的效果:<br>![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609247112340-1dcc1443-93e4-45e1-b9ff-4ed6ac6c412d.png#align=left&display=inline&height=263&margin=%5Bobject%20Object%5D&name=image.png&originHeight=525&originWidth=1212&size=104034&status=done&style=none&width=606)<br>**分析之后发现，解析结果依次为消息数组，请求游标，间隔时间，时间戳，和请求标志**

## 一、开始写protoc
![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609247126481-5ec0703e-4c6a-4b51-924d-54db485e4e4b.png#align=left&display=inline&height=234&margin=%5Bobject%20Object%5D&name=image.png&originHeight=467&originWidth=547&size=23690&status=done&style=none&width=273.5)

## 二、生成php类文件
运行：protoc --php_out=./ *.proto<br>![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609247142939-f718ccea-d3da-446a-aa35-5de1dd453c06.png#align=left&display=inline&height=104&margin=%5Bobject%20Object%5D&name=image.png&originHeight=208&originWidth=380&size=11151&status=done&style=none&width=190)

## 三、解析protoc文件
1.首先引入类库<br>2.调用mergeFromString方法解析<br>3.接下来就是调用get方法取参数了<br>![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609247158130-eb4c2020-8770-45ea-af5d-47100e4e06d3.png#align=left&display=inline&height=246&margin=%5Bobject%20Object%5D&name=image.png&originHeight=491&originWidth=727&size=53787&status=done&style=none&width=363.5)<br>4.运行效果：<br>![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1609247174245-f7ce5244-0e28-4be5-8087-9af151caa3c7.png#align=left&display=inline&height=421&margin=%5Bobject%20Object%5D&name=image.png&originHeight=841&originWidth=805&size=45046&status=done&style=none&width=402.5)<br>

> 更多短视频数据实时采集接口，请联系微信：ifuxing123



>
> 短视频、直播电商数据采集、分析服务，请联系微信：ifuxing123
> 免责声明：本文档仅供学习与参考，请勿用于非法用途！否则一切后果自负。
> 
