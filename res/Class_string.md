# [Class_string]字符串类的使用
字符串类是C++98标准里增加的，该类使用的时候必须包含头文件string，类名位于字符空间std中，使用时必须使用using命令或者使用std::string来使用它。字符串对象相对于字符串数组的最大优势在于其大小自动处理，很难出现访问非法地址的现象。
## 1.字符串对象的声明
```C++
string varname;
```
## 2.字符串对象的初始化
* 可以使用C风格的字符串初始化
* 可以直接将字符串常量赋值给字符串对象
```C++
string var1 = {"hello world!"};
string var2 = "hello world!";
```
## 3.字符串对象的基本操作
* 可直接赋值：字符串对象自动处理字符串的长度，而字符串对象主要着眼于字符串的存储单元
* 可直接使用加“+”进行拼接：使用操作符重载
* 可以直接与C风格字符串进行拼接
* 字符串大小可直接使用类内函数
```C++
string str1 = "Hello";
string str2 = "World";
string str3 = str1 + str2;
string str4 str1 + "World";
int strSize = str4.size();
```
## 4.其他
* 字符串数组在I/O时候每次读取一行而不是一个单词
* 还有其他格式的字符串

类型 | 使用方法 | 标识符 | 其他
---- | ---- |---- | ----
wchar_t | title[] = L"china"; | L | 无
char16_t | char16_t title[] = u"china"; | u | 无
char32_t | char32_t title[] = U"china"; | U | 无
原始类型 | R"(Hello \n Hi)" | R"()" | 与转义字符相对应 

