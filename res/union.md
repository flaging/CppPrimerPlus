# [union]联合体用法
联合体是一个特殊的数据结构，这个结构可以有多种数据类型，但在使用的时候每次只有一个数据类型。
```C++
struct widget{
    char band[20];
    int type;
    union {
        long id_num;
        char id_char[20];
    };

};
...
widget prize;
...
if(prize.type == 1){
    cin >> prize.id_val.id_num;
}
else{
    cin >> prize.id_val.id_char;
}
```
匿名公用体用法也类似。
```C++
struct widget{
    char band[20];
    int type;
    union id{
        long id_num;
        char id_char[20];
    }id_val;

};
...
widget prize;
...
if(prize.type == 1){
    cin >> prize.id_num;
}
else{
    cin >> prize.id_char;
}
```
