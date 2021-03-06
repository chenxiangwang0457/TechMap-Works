#	动态语言（弱类型）与静态语言（强类型）定义变量的区别
* 动态语言（强类型）：必须声明变量类型，之后才能对变量进行赋值。  
* 静态语言（弱类型）：不需要声明变量类型，但必须为变量赋值后才可以使用。  

  * 强类型：
  ```
       int x;
       x=200;   
  ``` 
  * 弱类型：
  ```  
       x=200  
  ```  
一般的强类型语言有C语言、C++、Java，弱类型语言有Python。

***

#	Python的基本数据类型
* Number（数字）：用来表示数据的一些数据  
   * int(整型)：python中的整数可以无限扩展  
   * float（浮点型）  
   * bool（布尔型）  
   * complex（复数型）  
* String（字符串）：用来表示文本的一些字符  
* List（列表）：用来表示一组有序的元素，后期还可以更改  
* Tuple（元组）：用来表示一组有序的元素，后期不可以更改  
* Sets（集合）：用来表示一组无序不重复的元组  
* Dictionary（字典）：用键值的形式保存一组元素  

***

# 任务task02
1.报错、什么原因？怎么得到结果3  
```  
	>>> a=input()  
	2  
	>>> b=1  
	>>> print(a)  
	2  
	>>> print(b)  
	1  
	>>> print(a+b)  
	Traceback (most recent call last):  
	File "<stdin>", line 1, in <module>  
	TypeError: can only concatenate str (not "int") to str  
	>>> a=int(a)  
	>>> print(a+b)  
```  

报错原因：运算时需要使用相同类型的数据，此时a为str，b为int，不可相加  
修改如上，对a进行数据类型转换，由str转换为int即可得到结果3，python中的input得到的数据的数据类型为字符串类型。  

***

2.b的值为abc  
```
	>>> a='abc'  
	>>> b=a  
	>>> a='def'  
	>>> print(b)  
	abc  
```

***

3.7/3与7//3的区别7//3与7.0//3的区别 原因？  
```  
	>>> 7/3  
    2.3333333333333335  
	>>> 7//3  
	2  
	>>> 7.0//3  
	2.0  
 ```  
Python中两数相除使用“/“时得到的是浮点型；使用”//“得到的是整形，最终输出的结果会舍去小数部分，返回数字序列中比真正的商小的最接近的数字，且如果有任何一个操作数是浮点数则返回一个浮点数。  

***

4.交换a，b的值并解释这样可行的原因  
 ```  
	>>> a=1  
	>>> b=2  
	>>> print(id(a))  
	140731213977248  
	>>> print(id(b))  
	140731213977280  
	>>> a,b=b,a  
	>>> print(a,b)  
	2 1  
	>>> print(id(a))  
	140731213977280  
	>>> print(id(b))  
    140731213977248  
```  
解释：python中的变量并不直接存值，而是引用了一个内存地址，在上述交换变量时只是快速交换了两个变量引用的内存地址。  

***

5.解释  
```  
	>>> a=600  
	>>> x=id(a)  
	>>> del a  
	>>> b=700  
	>>> y=id(b)  
	>>> x==y  
	True  
```  
详细的看一看：  
```  
	>>> a=600  
	>>> x=id(a)  
	>>> print(x)  
	2168428397200  
	>>> del a  
	>>> print(x)  
	2168428397200  
	>>> print(a)  
	Traceback (most recent call last):  
	File "<stdin>", line 1, in <module>  
	NameError: name 'a' is not defined  
	>>> b=700  
	>>> y=id(b)  
	>>> print(y)  
	2168428397200  
	>>> x==y  
	True  
```

解释：id（a），id（b）就是变量a，b所储存的内存地址  
或许下面的程序能比语言更好的解释吧（原谅我语言表达能力较差，但是实践出真知嘛）  
 ```  
	>>> num1=600  
	>>> print(id(num1))  
	2168428397360  
	>>> num2=700  
	>>> print(id(num2))  
	2168428397168  
	>>> num3=701  
	>>> print(id(num3))  
	2168428397456  
	>>> del num1  
	>>> num4=710  
	>>> print(id(num4))  
	2168428397360  
```  
可以发现，其实删除num1之前的num1和删除num1之后num4被储存在了同一个内存地址。

***

6.Python中实现自增自减  
Python中是没有++和--来实现自增自减的，查阅资料，原因是python的内部的存储空间分配机制和其他语言是不同的。例如当写下a=b=c=1时，三个变量的指针都指向同一个地方。而其他语言会给a,b,c分配三个不同的内存空间。  
故  
```  
	>>> i=1  
	>>> i++  
	File "<stdin>", line 1  
    i++  
      ^   
	SyntaxError: invalid syntax  
	>>> i--  
    File "<stdin>", line 1  
    i--  
      ^  
	SyntaxError: invalid syntax  
```  
若要实现其自增自减  
则有  
```  
	>>> i=1  
	>>> i=i+1  
	>>> i  
	2  
	>>> i=i-1  
	>>> i  
	1  
```  
但是在Python中确实存在--和++，如下  
```  
	>>> i=2  
	>>> i=--i  
	>>> i  
	2  
	>>> i=++i  
	>>> i  
	2  
```  
可以看到并没有像上面一样报错，我们来继续研究一下哈  
```  
	>>> i=-+i  
	>>> i  
	-2  
```  
所以好像python中--和++和-+好像只是一个符号问题，或者说是--即-1*-1，++=+1*+1，+-=+1*-1.查阅资料后，我发现确实是这个样子的。  

***

7.解释python中is和==的区别  
```  
	>>> a=[1,2]  
	>>> b=[1,2]  
	>>> a==b  
	True  
	>>> a is b  
	False  
	>>> print(id(a))  
	3120837588288  
	>>> print(id(b))  
	3120837656896  
```  
* 我先猜测，is就是判断id相同与否，==就是单纯判断值相同否，由此可以发现，a和b对应的内存的位置是不一样的，所以可能a is b 判断为False的原因就在此处。  
* 查阅资料可以知道：==是python标准操作符中的比较操作符，用来比较判断两个对象的value(值)是否相等  
而is也被叫做同一性运算符，这个运算符比较判断的是对象间的唯一身份标识，也就是id是否相同。  
由是可以验证我的猜测正确。  

***  

8.定义一个字符串 Let's go  
Python中字符串变量的定义非常简单，直接赋值即可。  
```
	>>> str="Let'go"  
	>>> print(str)  
	Let'go  
```
但是我发现当使用一般的单引号定义时居然会报错，如下  
```  
	>>> str='Let's go'  
	File "<stdin>", line 1  
    str='Let's go'  
             ^  
	SyntaxError: invalid syntax  
```  
* 这说明程序语法有问题，我注意到所定义的字符串中有‘这可能会影响程序，而Python中可以使用单引号、双引号、三引号进行定义，所以我尝试使用了双引号定义，发现程序可以正常输出。  
* 查阅资料：Python中如果字符串中包含单引号，就要使用双引号进行定义，一般情况下，三种引号并无区别。  

***

9.字符串'techf5ve' 从中截取出've'  
方法一：  
```  
	>>> str='techf5ve'  
	>>> print(str[-2:])  
	ve  
```  
解释：str[-2: ]表示从倒数第2个字符开始截取，一直到字符串的最后。  
方法二：  
```
	>>> str="techf5ve"  
	>>> print(str[6:8])  
	ve  
```  
* 切片的基本形式：切片操作基本表达式：object[start_index:end_index:step] ，只有一个“:”时，默认第三个参数step=1。  
* start_index：表示起始索引（包含该索引本身）；该参数省略时，表示从对象“端点”开始取值，至于是从“起点”还是从“终点”开始，则由step参数的正负决定，step为正从“起点”开始，为负从“终点”开始。  
* end_index：表示终止索引（不包含该索引本身）；该参数省略时，表示一直取到数据“端点”，至于是到“起点”还是到“终点”，同样由step参数的正负决定，step为正时直到“终点”，为负时直到“起点”。  
* step：正负数均可，其绝对值大小决定了切取数据时的‘‘步长”，而正负号决定了“切取方向”，正表示“从左往右”取值，负表示“从右往左”取值。当step省略时，默认为1，即从左往右以增量1取值。“切取方向非常重要!"（此段引用自<https://www.jianshu.com/p/15715d6f4dad>）   
* 查阅书籍（Python3.6零基础入门与实战 王启明 罗从良 著）知：start_index和end_index在某种意义上可以代替step。  