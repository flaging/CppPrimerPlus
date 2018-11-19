# [cin]cin的用法

cin是C++中一个基础的输入方式，通常的用法为

```C++
char var[varSize];
cin>>var;
```

## 1.cin使用时遇到分隔符便结束本次读入

当cin遇到空格、taby以及换行符号时，便会停止本次输入，如果仍有后续输入内容，这些内容会在输入缓冲区中以队列的形式存在，下次cin访问时直接取出来。

```C++
cout << "Enter your name:" << endl;
cin >> name;
cout << "Enter your favorite food:" << endl;
cin >> food;
cout << "your name is " << name <<" and your favorite food is " << food << endl;
```

该程序的实际运行情况为

```
Enter your name:
> Hello world
Enter your favorite food:
your name is Hello and your favorite food is world
```

经过空格后的world部分直接用作了下一次使用cin的输入。

## 2.发送给cin的输入时缓冲的，回车键按下后才会一起发送

在上一程序中，是在按下enter键以后Hello world才作为一个整体发送给cin，然后cin根据自己的断字规则读取相应内容。

## 3.cin的get()函数

这是istream类的一个成员函数，使用方式为

```C++
cin.get(var,varSize);
```

## 4.get()函数越过换行符的处理

get函数以换行符为界，但不对换行符作任何处理，故如果使用

```C++
cin.get(var1,varSize);
cin.get(var2,varSize);
```

由于第一次调用get时缓冲区队列的第一个元素为换行符，并不处理，var2读取时遇到的第一个元素就是换行符，所以var2读取不到任何输入。那么需要使用

```C++
cin.get(var1,varSize);
cin.get();
cin.get(var2,varSize);
```

这里使用不带参数的get函数实现读取下一个字符的作用(即使该字符为换行符)。

## 5.get()函数读取检查问题

可能会存在一个问题，输入的字符串长度大于设定的varSize值，那么可以通过查看下一字符的方式进行判断是由于数组满了还是遇到换行符才结束本次输入的。而下文中的getline()函数判断方式便没有这么简单了。

## 6.cin的getline()函数

getline()函数是新版本中才支持的一个函数。getline()函数与get()函数类似，唯一的区别是getline()函数会在保存数据的时候对换行符进行替换为空字符'\0'的操作。
所以可以使用

```C++
cin.getline(var1,varSize);
cin.getline(var2,varSize);
```

要注意的是，在这里的var1和var2都是一'\0'结尾的字符串。

## 7.失效位问题

get()函数在遇空行时会设置失效位（failbit），并阻断后续输出；同样的事情也会发生在getline()遇到数组满了的情况。
可以使用

```C++
cin.clear();
```

取消失效位。

## 8.混用各种输入的问题

例如下面的程序

```C++
cin >> var1;
cin.getline(var2,varSize);
```

这里的var2不会得到任何值，这是因为cin读取后将回车键的换行符留在输入缓冲区队列里。getline()读取的第一个字符就是换行符。
可以采用get()函数解决这一问题。也可以用下面方式

```C++
(cin >> var1).get();
```

## 9.cin字符循环输入

使用cin配合while实现字符的循环读入，并以#为结束符号。

```C++
char ch;
cin >> ch;
while( ch != '#'){
    cout << ch;
    //other opeartion
    cin >>ch;
}
```

上述方法能够读入所有字符，但依然无法正确读入空格、tab和换行。

## 10.cin.get(char)字符循环输入

```C++
char ch;
cin.get(ch);
while( ch != '#'){
    cout << ch;
    //other opeartion
    cin.get(ch);
}
```

可以处理空格tab和换行。

## 11.cin.get(char)读到文件结束

文件的结尾字符为EOF(End of File),可以使用cin.eof()来检测。当文件检测到EOF时，会将eof位置为1，同时failbit也会置1，所以也可以通过cin.fail()来检测。这两种方法都是事后检测。

```C++
char ch;
cin.get(ch);
while(cin.fail() == false){
    cout << ch;
    //other opeartion
    cin.get(ch);
}
```

也可以使用cin.clear()实现输入流的重置。
可以使用<CTRL>+<Z><ENTER>实现EOF符号的模拟。

## 12.判断方式的改进

3.中的

```C++
while(cin.fail() == false)
```

可以重写为

```C++
while(!cin.fail())
```

或者

```C++
while(cin)
```

最后一种方法还可以检测其他方面出错（如磁盘错误）导致的读取失败。
一种比较好的方式为

```C++
char ch;
while(cin.get(ch)){
    //do something;
}
```

## 13.另一个版本的读取方式

```C++
int ch;
ch = cin.get();
while(ch != EOF){
    //do something
    ch = cin.get()
}
```

以及

```C++
int ch;
while((ch = cin.get()) != EOF){
    cout.put(char(ch));
    //do something
}
```

## 14.cin 输入的本质

cin输入的时候，>>为运算符重载，其形参为引用，这是直接修改其值而不是拷贝的原因。

## 15.cin 输入报错

cin只能输入对应格式的输入流，不同格式的输入流会引起报错。

```C++
int sum = 0;
int input;
while(cin >> input){
    sum += input;
}
```

当输入为

```
1,2,3z,4
```

原程序只计算到3的值，因为z与int的格式不符。

标志位 | 作用 | 检测函数
---- | ---- | ----
eofbit | 文件尾标志 | eof()
badbit | 文件流是否破坏（如文件读取错误） | bad()
failbit | 是否读入或者输出预期字符 | fail()
goodbit | 是否正常 | good()

函数 | 作用 |函数 | 作用
---- | ---- | ---- | ----
rdstate() | 返回流状态 | exceptions() | 返回引发异常的状态
exception(isostate ex) | 设置哪些状态会引起clear()异常 | clear(iostate s) | 重置流状态
setstate( iostate s) | 设置状态位

## 16. 出错位的处理

可以使用如下的格式处理异常

```C++
while(cin >> input){
    //do something
}
if(cin.eof()){
    cout << "Loop terminated because of EOF" << endl;
    // do something
}
cin.clear(); //清除异常标志位，保证后续能继续读入
```

## 17.其他

* 存在一个ignore()函数
* 存在cin.get(var,varSize,'#')的用法

另，在fstream是iostream派生出来的，使用方法相似。
