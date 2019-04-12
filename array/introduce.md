第八章 数组

1 数组初始化

   使用const 声明数组

   const 把数组设置为只读 即：程序只能从数组中读 而不能写入新值

2  数组边界

  1  c 语言不会检查数组的下标是否合法 需要程序员自己判断
  2  给数组元素赋值

3  多维数组

    ex : 二维数组

        float rain[5][12] =
        {
            {1,2,3,4,5,6,7,8,9,0,1,2}
            {}
            {}
            {}
            {}

        }

4 数组与指针的关系

    float rain[10];

    !!! rain 的地址 与 rain[0] 的地址相同 数组名与数组首元素地址相同
    rain + 2  == &rain[2]   地址相同
    *(rain + 2) == rain[2]  值相同
    *(rain + 2) != *rain + 2  // * 的优先级高于 +
    rain[n] 可以定义为 到内存 rain 的位置 然后 移动 n 个单元 , 检索存储在那里的值

    注: 移动 n 个单元解释

    一个单元的大小由 指针变量的类型决定
    上例中 float 类型占用 4 个字节 ，那么一个单元 就为（四个字节），指针加一是指 单元加一 而不是下一个元素



5 函数的 数组形参

    函数原型的声明中 以下用法合法

    int sum(int ar[],int size);
    int sum(int [],int size);
    int sum(int *ar,int size);
    int sum(int *,int size);

    函数定义中 以下用法合法

    int sum(int *ar,int size);
    int sum(int ar[],int size);


6 使用指针形参

    我们可以使用两种方式来遍历数组

    foo.c

    函数处理数组必须要知道从什么时候开始 什么时候结束

    float rain[10] = {1,2,3,4,5,6,7,8,9,0};

    给定数组首元素地址 与数组元素个数
    foo1(rain,10)

    给定数组首元素 与 末尾元素下一位置 地址
    foo2(rain,rain+10)


7 指针表示法 与 数组表示法

    指针表示法:
        表达方式更加接近于机器语言、效率更高
    数组表示法：
        更容易理解、操作

8 常用指针操作

    指针赋值

        三种方式

        数组名
        &变量
        指针


    解引用

        *
    取址
        &
    指针与整数相加

        指针地址 + （整数 * （指针指向类型所占字节））

        int arr[5] = {1,2,3,4,5};

        arr[1] => *(arr + 1)


        如果超出数组有效范围 则计算结果是未定义的



    递增指针
        递增指向数组的指针 可以使指针指向数组的下一个元素

    指针减去一个整数
        可以使用 - 运算符使 指针减去一个整数
        但是指针必须为第一个运算对象 、整数是第二个运算对象

    递减指针
        回溯
    指针求差
        求差操作的两个指针一般为指向同一数组不同元素的两个指针
        用于求出两个元素之间的距离

    比较指针
        指针比较前提 两个指针指向相同类型的数据对象

    ----------------------------------------------------
    ！important
        千万不可以解引用未初始化的指针

        int *p;
        *p = 5;

        创建一个指针时 系统只分配了存储指针本身的内存 并未分配存储数据的内存（系统只记录了变量名，但是并未给该变量赋值  或者说并未将 地址 与 数据 映射起来）
        因此 在使用指针之前 必须先用已分配的地址初始化他（如果直接使用 获取到的结果将会是未知的）


        可能造成后果:
            1 擦写数据
            2 程序崩溃
    ----------------------------------------------------

8 保护数组中的元素

    在c的函数调用过程中 除 数组属于按址传递 其它全部都是按值传递 （数组按值传递需要产生数据对象副本 影响处理效率）

    按址传递操作会改变原始数据，为了保护原始数据 我们使用 const 关键字 修饰 数组为只读属性 ，通知编译器将 数组当做
    常量处理

     char * argv[] 代表这是一个 指向 char 类型数组的指针
     char * argv  代表这是一个指向char 字符的指针

     void main(int argc,char * argv[])  正确用法
     void main(int argc,char ** argv)  正确用法
     void main(int argc,char * argv)    错误用法


9  const

    const 数组
    const 指针
    指向const 的指针

10  指针与多维数组 （待完善）