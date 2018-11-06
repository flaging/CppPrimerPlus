# [vector]vector的用法
vector是用来替代数组的一个好的的数据结构，能够避免数组的一些问题。
## 1.vector的定义
```C++
#include <vector>
using std::vector;

vector <int> vi1;
vector <double> vi2;
vector <char> vi3;

//指定大小
vector <int> vi4(3);
vector <double> vi5(5);
vector <char> vi6(7);
vector <int> vi7(vi6);
```
> []运算符在本类中已经重载，可以使用数组的方法进行访问
## 2.vector的操作
函数名|作用 |函数名|作用
----|----|----|----
size()|返回vector元素个数|begin()|返回第一个元素的迭代器
end()|返回vector最后一个元素后的迭代器|push_back()|在尾部增加变量

