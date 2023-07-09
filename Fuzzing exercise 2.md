# Fuzzing exercise 2

## 环境准备 Ubuntu 20.04.2 LTS

username: fuzz

<p>password: fuzz

## 下载并构建目标

在得到模糊目标前为模糊项目创建一个目录

![image-20230709213823034](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709213823034.png)

下载libxif压缩包并进行解压

![image-20230709214557514](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214557514.png)

![image-20230709214615468](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214615468.png)

构建并安装libxif

![image-20230709214744249](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214744249.png)

![image-20230709214811146](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214811146.png)

![image-20230709214839197](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214839197.png)

![image-20230709214901711](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214901711.png)

![image-20230709214925242](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709214925242.png)

## 选择一个接口应用程序

libexif是一个库，用另一个应用程序来使用这个库，这个应用程序将被模糊化。

使用**exif命令行**。输入以下命令下载并解压缩exif命令行0.6.15

![image-20230709215144197](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215144197.png)

构建并安装exif命令行实用程序

![image-20230709215229927](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215229927.png)

![image-20230709215301307](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215301307.png)

![image-20230709215329280](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215329280.png)

![image-20230709215454122](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215454122.png)

![image-20230709215525683](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215525683.png)

![image-20230709215535552](C:\Users\15646\AppData\Roaming\Typora\typora-user-images\image-20230709215535552.png)

### 在此处出现问题，还在解决中
