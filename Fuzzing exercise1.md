# Fuzzing exercise1
## 环境准备 Ubuntu 20.04.2 LTS
<p>username: fuzz</p>
<p>password: fuzz</p>
下载并构建目标
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
安装AFL++
安装依赖项
<p><img width="415" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/bf47ee30-275e-46a5-8ae2-40e64e5c2768"></p>
<p><img width="369" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/6c4ef3ea-cdd9-4520-81f5-77c3b2701fea"></p>
<p><img width="362" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/27ed4844-df74-42cc-9b6b-d7c7fe99bbe9"></p>
构建AFL++
<p><img width="367" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/d7b85617-91b2-41a2-80e1-d15ba0a10d85"></p>
<p><img width="367" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/d7b85617-91b2-41a2-80e1-d15ba0a10d85"></p>
<p><img width="242" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/4c66183c-34bb-46ee-b008-e1b1ce70b535"></p>
<p><img width="361" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/233e6290-8b6e-42ff-8722-3debcb2889eb"></p>
<p><img width="416" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/f1b66699-a192-43f6-a954-e7716a33f920"></p>
<p><img width="272" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/b0ef1543-f015-487d-9f51-011395fafa21"></p>
<p>afl-fuzz查看是否安装成功</p>
<p><img width="379" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/28d2f364-f8b7-4319-aec9-8f7a13423e9e"></p>
<p>安装docker</p>
<p><img width="298" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/f7feaa09-caa0-4da7-970f-75373de2a56b"></p>
<p><img width="298" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/28fb0207-4cd5-473c-a64e-277ad8745eb0">
</p>
<p><img width="321" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/4def31b5-ed07-4b65-900e-58e9ebf9ed77">
</p>
<p>afl-fuzz查看是否安装成功</p>
<p><img width="379" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/5575e9e7-6282-4e65-a0d4-25573c60cdaa">
</p>
# 认识AFL++
<p>AFL是一个覆盖引导的模糊器，这意味着它收集每个突变输入的覆盖信息，以便发现新的执行路径和潜在的错误。当源代码可用时，AFL可以使用插装，在每个基本块(函数、循环等)的开头插入函数调用</p>
<p>要为我们的目标应用程序启用插装，我们需要使用AFL的编译器编译代码</p>
<p>首先，我们要清理所有之前编译过的目标文件和可执行文件</p>
<p><img width="336" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/1c27508c-20a1-468d-81e1-84673a408943">
</p>
<p>现在使用**afl-clang-fast**编译器构建xpdf</p>
<p><img width="415" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/697cbd2a-6f5d-4e6b-9eb7-a4e8f0c2205a">
</p>
<p><img width="253" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/c9b7bc7b-9fca-40dc-b137-3f6ceab1fdb9">
</p>
<p><img width="296" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/cf31c080-8204-427b-bdbf-ecf6ba8f2a00">
</p>
<p>运行fuzzer</p>
<p><img width="416" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/3dfb2666-b95a-44f3-9674-18502107b67b">
</p>
<p>每个选项的简要说明:</p>
<p>- *-i*表示我们必须放置输入大小写的目录(即文件示例)</p>
<p>- *-o*表示afl++存储修改后文件的目录</p>
<p>- *-s*表示使用静态随机种子</p>
<p>*@@*是AFL将用每个输入文件名替换的占位符目标的命令行</p>
<p>基本上，fuzzer会运行这个命令</p>
<p>$HOME/fuzzing_xpdf/install/bin/pdftotext <input-file-name> $HOME/fuzzing_xpdf/output '用于每个不同的输入文件。</p>
<p>由于收到消息 [-] Hmm...，进行如下操作</p>
<p><img width="415" alt="image" src="https://github.com/dbqyw/qyw.github.io/assets/130265921/fe83182b-385c-4ce6-9716-26cfefe63f32">
</p>
