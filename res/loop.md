# [loop]循环的使用

## 1.for循环的格式

```C++
for(initialization;test-expression;update expression){
    //循环体内容
}
//实际上，C++中的for格式为
for( for-init-statement condition;expression){
    //循环体内容
}
```

在for循环里面声明变量的一个好处是，一旦出了循环，变量就自动销毁了。

## 2.while循环的格式

```C++
while(test-expression){
    //循环体内容
}

do{
    //循环体内容
}
while(test-expression);
```

## 3.使用循环时的要点

* 设立终止条件
* 使用前初始化
* 使用后更新条件

## 4.C++11中基于范围的for循环

简化了for的使用条件，可用于数组、和向量容器、数组容器等元素。

```C++
for(int x : {1,2,3,4,5}){
    //循环体内容
    cout << x << endl;
}
```

## 5.break和continue在循环中的使用

```C++

for(auto x : {1,2,3}){  //point 1
    //循环体1
    if(test-expression){
        break;  //返回point 2
    }
    if(test-expression2){
        continue;  //返回point 1
    }
}
//point 2
```
