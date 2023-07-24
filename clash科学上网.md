登录clash官方网站
https://ikuuu.art/
（网站可能会挂，按照提示访问新域名）
在左侧**下载和教程**中选择**Linux使用教程**
1、在用户目录下创建clash文件夹
```text
mkdir clash
cd clash
```
2、下载clash二进制文件并解压，重命名为clash，存放在clash目录下
下载链接：
[Releases · Dreamacro/clash (github.com)](https://github.com/Dreamacro/clash/releases)
我下载的是**clash-linux-amd64-v3-v1.17.0.gz**
改名为clash.gz后解压为clash文件
```text
gzip -dv clash.gz
```
3、执行如下命令，下载clash配置文件
```text
wget -O config.yaml "https://api.sub-200.club/link/k726BxGA2nMeyL8V?clash=3"
```
4、启动clash，同时启动HTTP代理和Socks5代理，注意先修改权限
```text
chmod +x clash
./clash -d .
```
![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/7b3f3f8b-2b2f-4e19-88c4-8652235a1787)
5、访问[Clash (razord.top)](https://clash.razord.top/#/proxies)可以切换节点，测试延迟等操作
![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/7d6a0bd4-73fe-4f83-b06e-9d47b9e36f26)
6、打开系统设置，选择网络，点击网络代理右边的设置按钮，选择手动，修改HTTP和HTTPS代理，如下图所示
![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/3f10d15b-3067-4930-b328-233400d24af2)
可顺利访问外网
