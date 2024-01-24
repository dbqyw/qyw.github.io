# php变量规则

变量以$开始，后面跟着变量名称（不用声明变量类型）

```php
$text="helloworld"
$a=1
```

变量类型

```text
local
global 函数内访问全局变量
static 函数完成时，它的所有变量通常会删除，希望某个局部变量不被删除，就使用static关键字声明
```

输出 echo

输出变量

$txt1="学习 PHP";

$cars=array("Volvo","BMW","Toyota");

echo $txt1;

echo "< br >" 换行 

echo "我车的品牌是 {$cars[0]}";

输出print 和echo使用方法一样



PHP反序列化



public protected 子类可用

private 子类不可用

# php序列化

序列化的作用

序列化是将对象的状态信息（属性）转换为可以存储或传输形式的过程

对象 序列化为 字符串

将对象或数组转化为可存储/传输的字符串

在php中使用函数serialize()来将对象或者数组进行序列化，并返回一个包含字节流的字符串来表示



表达方式

```php
<?php
$a=null;
echo serialize($a);
?>
```

输出为N;



对象的序列化

```php
<?php
class test{
	public $pub="benben";
	function jineng(){
		echo $this->pub;
	}
}
$a=new test();
echo serialize($a);
?>
```

不能序列化类，可以序列化对象，输出为：

`O:4:"test":1:{s:3:"pub";s:6:"benben";}`

`O(object):4(类名长度):"test"(类名):1(变量数量):{s:3(变量名字长度):"pub"(变量名字);s:6(值的长度):"benben"(变量值);}`

private私有属性序列化时，在变量名前加"%00类名%00"，但是直接看看不见

要先加上这个，再对私有属性进行反序列化

# php反序列化

反序列化的特性

1、反序列化之后的内容为一个对象

2、反序列化生成的对象里的值，由反序列化里的值提供，与原有类预定义的值无关

3、反序列化不触发类的成员方法，需要调用方法后才能触发

[3 先反序列化，再调用类里面的成员方法，类不能被注释，否则找不到成员方法]

反序列化 unserialize

反序列化就是将序列化后的参数还原成实例化的对象

序列化  serialize

反序列化漏洞的成因：反序列化过程中，unserialize()接收的值（字符串）可控；通过更改这个值（字符串），得到所需要的代码，即生成的对象的属性值

通过调用方法，出发代码执行

eval()执行代码

# 魔术方法

魔术方法是一个预定义好的，在特定情况下自动触发的行为方法

魔术方法的作用

反序列化漏洞成因：反序列化过程中，unserialize()接收的值（字符串）可控，通过更改这个值（字符串）得到所需要的代码，通过调用方法，出发代码执行

魔术方法在特定条件下自动调用相关方法，最终导致触发代码

魔术方法触发时机，参数，返回值

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/ac512080-8094-4f8e-91bf-a4967df8ada4)

## __construct()

**__construct()** 构造函数，在实例化一个对象的时候，首先会去自动执行的一个方法

触发时机：实例化对象

功能：提前清理不必要内容

参数：非必要

返回值

在序列化和反序列化过程中不会被触发

## __distruct()

**__distruct()** 析构函数，在对象的所有引用被删除或者当对象被显式销毁时执行的魔术方法

实例化对象结束后，代码运行完会销毁，触发构造函数__destruct()

触发时机：对象引用完成，或对象被摧毁

功能：

参数：

返回值

在序列化过程中不会被触发

在反序列化过程中会触发，反序列化得到的是对象，用完后会销毁，触发析构函数__distruct()

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/a4b6409a-6b95-4a39-8f26-7e5078d66760)

## __sleep()

**__sleep()** 序列化serialize()函数会检查类中是否存在一个魔术方法__sleep()，如果存在，该方法会现被调用，然后才执行序列化操作，此功能可以用于清理对象，并返回一个包含对象中所有应被序列化的变量名称的数组，如果该方法未返回任何内容，则NULL被序列化，并产生一个E_NOTICE级别的错误

触发时机：序列化serialize()之前

功能：对象被序列化之前触发，返沪需要被序列化存储的成员属性，删除不必要的属性

参数：成员属性

返回值：需要被序列化存储的成员属性

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/ac24a1bf-aa25-4408-81f9-5e493226c41a)

__sleep执行返回需要序列化的变量名，过滤掉password变量

serialize()只序列化sleep返回的变量

## __wakeup()

**__wakeup()** unserialize()会检查是否存在一个__wakeup()方法，如果存在，则会先调用__wakeup()方法，预先准备对象需要的资源。

预先准备对象资源，返回void，常用于反序列化操作中重新建立数据库连接或执行其他初始化操作

触发时机：反序列化unserialize()之前

功能：

参数：

返回值：

__wakeup()在反序列化unserialize()之前

__destruct()在反序列化unserialize()之后

有的题要绕开它们，避免值被改变

## __toString()

**__toString()** 表达方式错误导致魔术方法触发

触发时机：把对象当成字符串调用

功能：

参数：

返回值：

把类User实体化并赋值给$test，此时$test是个对象，调用对象可以使用print_r或者var_dump

如果使用echo或者print只能调用字符串的方式去调用对象，即把对象当成字符串使用，此时自动触发toString()

## __invoke()

**__invoke()** 表达方式错误导致魔术方法触发

触发时机：把对象当成函数调用

功能：

参数：

返回值：

把类User实体化并赋值给$test，此时$test是个对象，调用对象可以使用print_r或者var_dump

加()是把test当成函数test()来调用，此时触发invoke()

$test()

## __call()

**__call()** 

触发时机：调用一个不存在的方法

功能：

参数：2个参数传参$arg1,$arg2（参数个数与定义的__call()函数相对应）

返回值：调用的不存在的方法的名称和参数

调用的方法不存在，触发魔术方法__call()

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/1620df34-063d-47b4-bd90-4e8dee8f2d4a)

## __callStatic()

**__callStatic()** 

触发时机：静态调用或调用成员常量时使用的方法不存在

功能：

参数：2个参数传参$arg1,$arg2（参数个数与定义的__callStatic()函数相对应）

返回值：调用的不存在的方法的名称和参数

调用的方法不存在，触发魔术方法callStatic()

静态调用 $test :: callxxx('a')

非静态调用 $test -> callxxx('a')

## __get()

**__get()** 

触发时机：调用的成员属性不存在

功能：

参数：传参$arg1

返回值：不存在的成员属性的名称

var2不存在

$test -> var2;

__get($arg1)

把var2赋值给$arg1

最后输出var2

## __set()

**__set()** 

触发时机：给不存在的成员赋值属性

功能：

参数：传参$arg1,$arg2

返回值：不存在的成员属性的名称和赋的值

## __isset()

**__isset()** 

触发时机：对不可访问属性使用isset()或empty()时，__isset()会被调用

功能：

参数：传参$arg1

返回值：不存在或不可访问的成员属性的名称



![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/f77d9eb7-790b-4a2b-a9e5-7ce6ac2c78ae)

## __unset()

**__unset()** 

触发时机：对不可访问属性使用unset()时

功能：

参数：传参$arg1

返回值：不存在的成员属性的名称

## __clone()

**__clone()** 

触发时机：当使用clone关键字拷贝完成一个对象后，新对象会自动调用定义的魔术方法__clone()

功能：

参数：

返回值：

## 魔术方法总结

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/a5f1cfa7-8a39-4006-9da5-e88d05037ac6)

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/1d20ae88-8cf7-445d-b8b8-9ee1fe9cbf57)

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/87ebba2f-9a57-438b-b175-9a05684e6fd5)

# POP链构造，POC编写

**POP链**

在反序列化中，我们能控制的数据就是对象中的属性值（成员变量），所以在PHP反序列化中有一种漏洞利用的方法叫”面向属性编程“，即POP

POP链就是利用魔法方法在里面进行多次跳转然后获取敏感数据的一种payload

**POC编写**

POC中文译作概念验证，在安全界可以理解成漏洞验证程序，POC是一段不完整的程序，仅仅是为了证明提出者的观点的一段代码

编写一段不完整的程序，获取所需要的序列化字符串

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/664dfe0f-e131-4c81-bce1-8b586adaa113)

要触发Modifier的append得到flag，value=flag.php

要触发Modifier的__invoke()  把对象当成函数调用

触发Test的__get()  给不存在的成员属性赋值，p赋值为Modifier对象，就能return对象

然后触发get，给不存在的成员属性赋值，给Show中的$str赋值为Test属性，

然后需要触发__wakeup，反序列化之前，在wakeuo中，让source为Show对象，一定要是Show的对象，否则无法触发tostring

再把对象当字符串用，就能触发tostring

# 字符串逃逸基础_字符减少

反序列化分隔符

反序列化以;}结束，后面的字符串不影响正常的反序列化

属性逃逸

一般在数据先经过一次serialize再经过unserialize，再这个中间反序列化的字符串变多或者变少的时候有可能存在反序列化属性逃逸

构造值，让倒数第二个“及之前的功能性代码变为值，则后面的值变成功能性代码

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/34903358-33f5-461a-a413-eea3b32c0dc9)

反序列化字符串逃逸：多套一处一个成员属性，第一个字符串减少，吃掉有效代码，在第二个字符串构造代码

# 字符串逃逸基础_字符减增多

反序列化字符串减少逃逸：多逃逸出一个成员属性，第一个字符串减少，吃掉有效代码，在第二个字符串构造带吗

反序列化字符串增多逃逸：构造出一个逃逸成员属性，第一个字符串增多，吐出多余代码，把多余位代码构造成逃逸的成员属性

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/b6508253-d62e-4cd4-a60d-b5e830250f9b)

第一个字符串增多，吐出多余代码，把多余代码构造成逃逸成员属性

**字符串逃逸增多，例题思考**

profile是test对象，且pass值为escaping

把$name中的$safe替换为hack

__construct()实例化对象时会触发

实例化test对象时会触发__construct，把$param的值赋给test对象的user

然后反序列化时，会把$param中的flag和php都转为hack

要改变pass的值，但是分析一遍过后发现没有对pass进行更改，因此利用filter中将php替换为hack，字符串逃逸，字符增多，把有效代码往外吐

";s:4:"pass";s:8:"escaping";}

要吐出29个

所以要29个php替换为hack

**字符串逃逸减少，例题思考**

要让$profile->vip为true，才能输出flag

题目要获取user和pass

param为user

user和pass的值为test类的user和pass值

filter是把flag和php替换为hk

字符串减少，把后面的包进来

要变成功能性代码的

s:4:"user";s:?:"fff";s:4:"pass";s:25:"1";**s:3:"vip";s:4:"true";}**"

前面要包住20个，flag包2，php包1

10个flag

?user=flagflagflagflagflagflagflagflagflagflag &pass=1";s:3:"vip";b:1;}

O:4:"test":3:{s:4:"user";s:4:"flag";s:4:"pass";s:6:"benben";s:3:"vip";b:1;}

# wakeup绕过

反序列化漏洞：CVE-2016-7124

漏洞产生原因：如果存在__wakeup方法，调用unserilize()方法之前

会先调用__wakeup方法，但是序列化字符串中表示对象属性个数的值大于真实的属性个数时

会跳过__wakeup()的执行

把成员属性数量+1，就能绕过__wakeup()

如果题目中正则表达式，不允许O后面跟数字，就写成O:+6

```
'/[oc]:\d+:/i'
```

例如：

$a = 'O:+6:"secret":2:{s:4:"file";s:8:"flag.php";}';

echo urlencode($a);

记得最后要urlencode一下

# 引用

符号&

$a->enter=&$a->secret

保证$a->enter的值和$a->secret的值一直一样

# session反序列化漏洞

当session_strat()被调用或者php.ini中session.auto_start为1时，PHP内部调用会话管理器，访问用户session被序列化以后，存储到指定目录（默认为/tmp）

存取数据的格式有多种，常用的由三种

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/d66a2d5a-cef5-403c-8f53-509e07146229)

漏洞产生：写入格式和读取格式不一样  

当网站序列化并存储session，与反序列化并读取session的方式不同，就可能导致session反序列化漏洞的产生。

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/034b1373-ca69-4b5c-9212-8488505fcc51)

![image](https://github.com/dbqyw/qyw.github.io/assets/130265921/34ca214d-e437-4039-8876-cf507964ecbc)
