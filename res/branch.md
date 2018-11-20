# [branch]分支的用法

## 1.分支语句的结构

```C++
//if 语句
if(test-condition){
    statement;
}

//if-else 语句
if(test-condition){
    statement1;
}
else{
    statement2;
}

//if-elseif 语句
if(test-condition1){
    statement1;
}
else if(test-condition2){  //实际是两个if-else 的嵌套
    statement2;
}
else{
    statement3;
}

//switch-case 语句
switch(interger-expression){
    case label1 : {statement1;break;}
    ...
    default : {statementn;}
}
```

## 2.选择语句中的地雷

* 通常使用value == variable来避免出现赋值语句的现象
* 可以使用枚举类型作为switch-case的interger-expression
* 在switch-case的过程中，需要配合break或者continue使用
