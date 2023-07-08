# Fuzzing exercise1
## 环境准备 Ubuntu 20.04.2 LTS
<p>username: fuzz</p>
<p>password: fuzz</p>
## 下载并构建目标
<p>首先得到模糊目标。为要模糊化的项目创建一个新目录</p>
<img width="317" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/d948710c-406b-4972-a182-d657efcf1d4e">
<p>安装一些额外的工具(make和gcc)，使环境完全准备好</p>
<p>首先要更新apt</p>
<p><img width="337" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/15e9567e-b482-4d1e-bf79-cfd581e3d76a"></p>
<p><img width="347" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/ee66a031-3b16-4129-8804-d1e0b72d1c70"></p>
<p>下载Xpdf 3.02并解压</p>
<p><img width="363" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/80d747b9-4574-4f52-8d98-3236bc36e0b6"></p>
<p><img width="331" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/73185429-6879-4656-861f-2bcf2ffd202c"></p>
<p>构建Xpdf</p>
<p><img width="361" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/39cce4fe-dde6-4304-9a28-fbde1e4fbb73"></p>
<p><img width="363" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/8510a266-ce8d-450d-9eea-b5535d803fd4"></p>
<p><img width="261" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/d17eb6d0-c211-4fdb-9172-ef5a484eda6f"></p>
<p><img width="297" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/25698387-3fe4-4d5e-9ebe-93a4423755fe"></p>
<p>下载一些PDF来测试构建是否成功</p>
<p><img width="359" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/63f75383-8647-430a-8b94-735832b90b8e"></p>
<p><img width="366" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/7b3b8e29-3f1f-4456-a297-ab3582a0e9da"></p>
<p>开始测试</p>
<p><img width="365" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/e272064c-14c6-4521-bc84-603e9de43a44"></p>
<p><img width="359" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/ffb59f24-fbe8-43a6-8b67-f43345a99416"></p>
## 安装AFL++
安装依赖项
<p><img width="415" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/bf47ee30-275e-46a5-8ae2-40e64e5c2768"></p>
<p><img width="369" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/6c4ef3ea-cdd9-4520-81f5-77c3b2701fea"></p>
<p><img width="362" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/27ed4844-df74-42cc-9b6b-d7c7fe99bbe9"></p>
 构建AFL++
<img width="367" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/d7b85617-91b2-41a2-80e1-d15ba0a10d85">
<img width="242" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/4c66183c-34bb-46ee-b008-e1b1ce70b535">
<img width="361" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/233e6290-8b6e-42ff-8722-3debcb2889eb">
<img width="416" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/f1b66699-a192-43f6-a954-e7716a33f920">
<img width="272" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/b0ef1543-f015-487d-9f51-011395fafa21">
<p>afl-fuzz查看是否安装成功</p>
<img width="379" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/28d2f364-f8b7-4319-aec9-8f7a13423e9e">
