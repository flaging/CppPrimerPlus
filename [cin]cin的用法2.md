# [cin]cin的用法2
## 1.cin字符循环输入
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
## 2.cin.get(char)字符循环输入
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
## 3.cin.get(char)读到文件结束
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
## 4.判断方式的改进
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
    //do something 
}
```
## 5.另一个版本的读取方式
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
## 6.cin 输入的本质
cin输入的时候，>>为运算符重载，其形参为引用，这是直接修改其值而不是拷贝的原因。
## 7.cin 输入报错
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
## 7. 出错位的处理
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
## 8.其他
* 存在一个ignore()函数
* 存在cin.get(var,varSize,'#')的用法

另，在fstream是iostream派生出来的，使用方法相似。
