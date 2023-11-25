##Some points in C Programming
####**Week1**
P1.C语言的标识符由字母、数字和其他任意字符组成。(T/F)
<details>
<summary>answer & analysis</summary>
F.应当由字母、数字和下划线组成，其中首字符不能为下划线。实际运行中，包含 $ 的标识符(identifier) 也可以编译通过。在这样的标识符中，$ 字符也可以作为首字符。
</details>
<br/>
P2.

    int n=5,x;
    x=n++;
    the value of x will be 5. (T/F)
<details>
<summary>answer & analysis</summary>
T.n变为6实际上是n++的side effect，在此之前已经将n的值赋给x。
</details>
<br/>
P3.

    int k=2;
    while (k=0){
        printf("%d",k);
        k--;
    }
while循环执行()次。
<details>
<summary>answer & analysis</summary>
0.while (k=0)中条件表达式值为0，while循环不执行。（若改为while (k=1)，则为无限循环。）
</details>
<br/>

<br/>

####Week3
P1.The following text is part of error information threw by the compiler when compiling some buggy C program.
**Id:symbol(s) not found for architecrture x86-64
clang:error:linker command failed with exit code 1**
Which of the following problems exist in the C program is related to the information?
A.Some variable is used without definition.
B.A neccessary semicolon ';' is missing.
C.The program does not include the header file **stdio.h** but uses function **printf**.
D.The only function in the program is named **mian**.
<details>
<summary>answer & analysis</summary>
D.链接器会默认以名字为main的函数作为入口，则此时链接器会因为找不到main函数而出错。（事实上编译器不报错。）
</details>
<br/>

P2.对于定义int a[5];可以通过语句scanf("%d",a);输入全部元素的值。(T/F)
<details>
<summary>answer & analysis</summary>
F.这不同于char a[5]。
</details>
<br/>

P3.以下代码，语法正确的是：

    A.while ( ) ;
    B.for ( ) ;
    C.for (;;) ;
    D.do { } while ( );

<details>
<summary>answer & analysis</summary>
C.";"是一个空语句。
</details>

<br/>
<br/>

####Week4
P1.sizeof()是C语言的一个函数，可以计算参量所占内存的字节数。如sizeof(int)可计算整型所占的字节数。(T/F)
<details>
<summary>answer & analysis</summary>
F.sizeof是关键字而不是函数。sizeof的两种用法：sizeof (类型)、sizeof 表达式。
</details>
<br/>

P2.C语言中，通过函数调用只能获得一个返回值。(T/F)
<details>
<summary>answer & analysis</summary>
F.函数调用获得的返回值为0或1个。
</details>
<br/>

P3.在C语言程序中，若对函数类型未加显式说明，则函数的隐含类型为（）。

    A.void
    B.double
    C.char
    D.int

<details>
<summary>answer & analysis</summary>
D.
</details>

<br/>
<br/>

####Week5
P1.以下说法正确的是：

    A.一个C语言（源文件.c文件）必须包含main函数
    B.一个C语言源文件（.c文件）可以包含两个以上main函数
    C.C语言头文件（.h文件）和源文件（.c文件）都可以进行编译
    D.在一个可以正确执行的C语言程序中，一个C语言函数的声明（原型）可以出现任意多次。

<details>
<summary>answer & analysis</summary>
C.这题可能错选A，事实上多文件编程时，只需要一个.c文件包含main函数即可。
</details>

<br/>

####Week6
P1.Among the following C code segments,which one generates the following error when compiling?
**error:implicit declaration of funciton is invalid in C99**

A.

    int my_pow(int a,int b)
    int main()
    {
        int a = my_pow(2,6);
    }
B.

    int my_pow(int a,int b) {}
    int main()
    {
        int a = my_pow(2,6);
    }
C.

    int main()
    {
        int a = my_pow(2,6);
    }
    int my_pow(int a,int b) {}
D.

    int my_pow(int a,int b);
    int main()
    {
        int a = my_pow(2,6);
    }
    int my_pow(int a,int b) {}
<details>
<summary>answer & analysis</summary>
C.在C语言中，当调用一个在调用时尚未被声明的函数时，编译器会给出implicit declaration of function的error报错，属于编译阶段错误，只有C项符合在调用时尚未声明；当某个被调用的函数只有声明没有定义时会给出Undefined symbols、symbol(s) not found等error报错，但这种报错本质是链接错误(linker command failed with exit code 1)，是在编译完成后链接阶段的错误，A项会报此错；当某个返回值类型不为void的函数没有返回值时，编译器一般之报warning或者不报错，不会报error。如果调用了该函数并取得返回值，一般取得一个不确定值，B、D项会出现这种情况。
</details>

<br/>

P2.Among these definition of 2-d arrays,which is/are correct?
A.int a[1][2];
B.int a[][2];
C.int a[][2] = {0};
D.int a[][2] = {0,1,2,3,4};
E.int a[][2] = {{0,1},{2,3},};
F.int a[2][] = {{0,1},{2,3}};
<details>
<summary>answer & analysis</summary>
ACDE.
A项创建一个1*2的二维数组，没问题；

B项创建的数组大小未知，不能通过编译；
C、D项创建一个2列（第一维）若干行（第二维）的二维数组，行数由初始化时给定的元素个数决定，未填满的元素填0，没问题；
E项是正常的二维数组初始化方式，末尾的逗号无关紧要，没问题；
F项没有确定数组第一维的大小，不能通过编译。
</details>

<br/>



<br/>
<br/>
<br/>

优先级|运算符|结合性/目数
-|:-:|-:
1|[]数组()|/
1|->结构|/
2|-取负 ++ --|右/单
2|（类型）|右
2|* &指针/地址|右/单
2|!非 ~按位反|右/单
2|sizeof|右
3|* / %|/双
4|+ -|/双
5|<< >>|/双
6|>(=) <(=)|/双
7|== !=|/双
8/9/10|&/^/\|位|/双
11/12|&& \|\||/双
13|?:|右/三
14|赋值|右
15|,|/




<br/>
<br/>
<br/>
<br/>


#####translation:
argument参数(实参？)
parameter参数（形参？）
recursion递归
sub expression子表达式





<br/>
<br/>




#####*several tiny points:*
1. 关于运算符",":逗号运算符会顺序执行一系列运算。整个逗号表达式的值是以逗号分隔的列表中最后一个表达式的值。
