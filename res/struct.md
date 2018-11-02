# [struct]结构体用法
结构体是C++类实现的基石。
## 1.结构体的声明和定义
在声明过程中注意最后有一个分号作为结尾。同时，在C++中定义的时候可以省略关键词struct。struct结构也可以定义函数，与类不同之处在于所有内容默认都是public的。
```C++
struct person{
    char name[10];
    double height;
    };

person Xiaoming;
```
结构体的声明与变量作用域的规定类似，当结构声明在外部时，其结构体变量由外部共享，局部声明的结构体其变量只在局部可用。通常鼓励在外部进行结构体的声明，以保证所有的函数都可以访问该函数。
## 2.结构体的初始化和访问
```C++
person Xiaoming = {"xiaoming",1.70};
person Xiaogang {"xiaogang",1.90};  //可以省略赋值号
person Xiaopeng = Xiaoming; //可以直接赋值
person Xiaohong {};  //所有值均为零

double xiaomingHeight = Xiaoming.height;
```
需要注意的是：
* 结构体赋值过程中不允许缩窄转换(损失精度的转换)
* 结构体变量间可以直接赋值
* 结构体初始化时为空，那么所有值均为零
## 3.结构体作为函数参数和返回值
结构体在作为参数和返回值的时候，其处理与基本变量相同，既可以使用值传递的方式，也可以使用地址传递的方式。
## 4.结构数组
```C++
person group[10];  //定义
group[0].height = 1.65;  //访问值
person group2[2] = {  //定义与初始化
    {"xiaoming",1.55},
    {"xiaogang",1.80}
};
group.height =0;  //不符合要求的使用方法
```
## 5.位字段
使用位字段可以将结构体与特定的硬件寄存器位数相匹配，避免造成内存的浪费。
```C++
struct test{
    unsigned int SN : 4;  //SN占4位
    unsigned int :4;  //4位没有使用
    bool goodIn : 1;  //输入成功标志位1位
    bool goodTorgle : 1;  //未用
}
```
## 6.匿名结构体
无法显示表示其类型。
```C++
struct {
    int x;
    int y;
} position;
```
定义一个名为position的结构体实例，这类结构体无法新建同类对象。可以在定义时候直接赋值。
```C++
struct {
    int x;
    int y;
} position ={
    1,1
};
```
