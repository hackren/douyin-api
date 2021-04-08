# 抖音数据采集Frida脱壳工具


>
> 短视频、直播电商数据采集、分析服务，请查看文档： [TitoData](https://www.titodata.com?from=douyinarticle)
> 免责声明：本文档仅供学习与参考，请勿用于非法用途！否则一切后果自负。
> 

## 概述
现在很多 `app` 都会对 `Frida` 进行检测，所以要根据app的情况来具体使用

## 壳的分类
壳的种类非常多，可以简单的分为以下三类：

- 一代整体型：采用Dex整体加密，动态加载运行的机制（免费类的壳）；
- 二代函数抽取型：将方法单独抽取出来，加密保存，解密执行（某加密）；
- 三代VMP、Dex2C：独立虚拟机解释执行。

## Frida-Unpack
> firda-unpack 原理是利用frida hook libart.so中的OpenMemory方法，拿到内存中dex的地址，计算出dex文件的大小，从内存中将dex导出，我们可以查看项目中的 OpenMemory.js 文件中的代码更清晰直观地了解。

参考文献： [https://bbs.pediy.com/thread-258776.htm](https://bbs.pediy.com/thread-258776.htm)<br>GitHub地址：[https://github.com/GuoQiang1993/Frida-Apk-Unpack](https://github.com/GuoQiang1993/Frida-Apk-Unpack)<br>[![](https://cdn.nlark.com/yuque/0/2021/png/97322/1611487409463-13118cad-1570-4bd8-90d7-5bc03c62eaa3.png#align=left&display=inline&height=547&margin=%5Bobject%20Object%5D&originHeight=547&originWidth=718&size=0&status=done&style=none&width=718)](https://static.zhangkunzhi.com/typecho/2020/08/20/953524246794930/1597895351.png)<br>将 `dex` 文件并 `dump` 下来，保存在 `data/data/packageName` 目录下

## FRIDA-DEXDump
> 葫芦娃所写，脱壳后的dex文件保存在PC端main.py同一目录下，以包名为文件名

GitHub地址：[https://github.com/hluwa/FRIDA-DEXDump](https://github.com/hluwa/FRIDA-DEXDump)<br>[![](https://cdn.nlark.com/yuque/0/2021/png/97322/1611487409403-a57a3c0b-daea-4e40-8bbb-1eadc1688d7b.png#align=left&display=inline&height=283&margin=%5Bobject%20Object%5D&originHeight=283&originWidth=939&size=0&status=done&style=none&width=939)](https://static.zhangkunzhi.com/typecho/2020/08/20/954871491878402/1597895486.png)

## frida_dump
> 文件头搜索dex，来脱壳

会搜索 `dex` 文件并 `dump` 下来，保存在 `data/data/packageName/files` 目录下<br>GitHub地址：[https://github.com/lasting-yang/frida_dump](https://github.com/lasting-yang/frida_dump)<br>[![](https://cdn.nlark.com/yuque/0/2021/png/97322/1611487409468-c52384db-3d2b-4606-bcee-c7f53c04f5a8.png#align=left&display=inline&height=411&margin=%5Bobject%20Object%5D&originHeight=411&originWidth=911&size=0&status=done&style=none&width=911)](https://static.zhangkunzhi.com/typecho/2020/08/20/955723917172999/1597895571.png)

## Frida_Fart[推荐]
> 寒冰写的， Frida 版的 Fart, **目前只能在 andorid8 上使用**该frida版fart是使用hook的方式实现的函数粒度的脱壳，仅仅是对类中的所有函数进行了加载，但依然可以解决绝大多数的抽取保护

GitHub地址：[https://github.com/hanbinglengyue/FART](https://github.com/hanbinglengyue/FART) 下载 `frida_fart.zip` 即可

1. 解压 `frida_fart.zip`
1. 将目录中的 `fart.so` 与 `fart64.so` 推送到 `/data/app目录下` 并使用 `chmod 777`
1. 需要以spawn方式启动app，等待app进入Activity界面后，执行fart()函数即可。如app包名为com.example.test,则
```
frida -U -f com.example.test -l frida_fart_hook.js --no-pause
```
**Shell**<br>_ 复制_

1. 等待app进入主界面,执行fart()
> 高级用法：如果发现某个类中的函数的CodeItem没有dump下来，可以调用dump(classname),传入要处理的类名，完成对该类下的所有函数体的dump,dump下来的函数体会追加到bin文件当中。

**于被动调用的脱壳修复，由于代码覆盖率低，不可能触发app中的所有函数的调用，因此，修复的范围有限。**
