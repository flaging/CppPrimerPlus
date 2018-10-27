# [cin]cin的用法
cin是C++中一个基础的输入方式，通常的用法为
```C++
int var;
cin>>var;
```
## 1.cin使用时遇到分隔符便结束本次读入
当cin遇到空格、taby以及回车符号时，便会停止本次输入，如果仍有后续输入内容，这些内容会在输入缓冲区中以队列的形式存在，下次cin访问时直接取出来。
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


