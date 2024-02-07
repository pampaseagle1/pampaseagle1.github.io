## Some points in C Programming
### Week1
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

### Week3
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

### Week4
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

### Week5
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

### Week6
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

### Week10
Some points:
1.Array as a parameter is pointer.But it can be used with operator[],which makes it look like an array.So the four prototypes below are equal:

    int sum(int *a,int n);
    int sum(int *,int n);
    int sum(int a[],int n);
    int sum(int [],int n);
<br/>
2.Array variable is const pointer,that's why it cannot be assigned.
<br/>
P1.关于C语言指针的运算：指针只有加减操作，没有乘除操作。指针可以加常数、减常数；相同类型的指针可以相加、相减。(T/F)
<details>
<summary>answer & analysis</summary>
F.相同类型的指针可以做减法表示他们的距离，而相加没有意义。
</details>
<br/>

P2.假设有定义如下： int array[10]; 则该语句定义了一个数组array。其中array的类型是整型指针（即： int *）。(T/F)
<details>
<summary>answer & analysis</summary>
F.array的类型是数组名。注意array存储的是array[0]的地址，array代表的是整个数组，因此&array和array虽然数值相同，但意义不同。(&array)+1会使地址向后移动40个Byte，而array+1只会移动4个Byte。
<br/>
另一种方法：考虑sizeof。sizeof(array)显然是40，而对于整型指针变量int *p,sizeof(p)=8.
</details>
<br/>
P3.If variables are defined and assigned correctly, the expression ______ is wrong.

A.a&b
B.a^b
C.&&x
D.a, b

<details>
<summary>answer & analysis</summary>
C. &x已经得到了x的地址，而(&x)是直接访问到的，并没有存储在某个变量中，所以&(&x)的操作是无效的。
</details>
<br/>
P4.According to the declaration: int a[10], *p=a; the expression __ is wrong.

A.a[9]
B.p[5]
C.*p++
D.a++
<details>
<summary>answer & analysis</summary>
D.数组名可以看作常量指针，不能进行++操作。
</details>
<br/>
P5. Among the following assignments or initializations, __ is wrong.

A.char str[10]; str="string";
B.char str[]="string";
C.char *p="string";
D.char *p; p="string";
<details>
<summary>answer & analysis</summary>
A. 字符数组只能在定义时才能用字符串字面量初始化，定义后不行。字符串在被定义时和定义后都能这么干。
</details>
<br/>

P6. According to the declaration: int (*p)[10];, p is a(n) __.
A.pointer
B.array
C.function
D.element of array
<details>
<summary>answer & analysis</summary>
A.p是一个指针，指向若干长度为10的一维数组。
</details>
<br/>
P7.Among the following statements, __ is equivalent to the declaration: int *p[4];.

A.int  p[4];
B.int  **p;
C.int  *(p[4]);
D.int  (*p)[4];
<details>
<summary>answer & analysis</summary>
C. []的优先级高于*。注意这里C、D选项的区别，前者是四个指针构成的指针数组，后者是指向长度为4的数组的指针。

此外，int (*p)[4]的类型是(int *)[4],这与int **p不同。
</details>
<br/>
P8.For the function declaration void f(char ** p)，the definition __ of var makes the function call f(var) incorrect。

A.char var[10][10];
B.char *var[10];
C.void *var = NULL;
D.char *v=NULL, **var=&v;
<details>
<summary>answer & analysis</summary>
A。A 中 var 的类型是二维数组，传参时的类型为 (*char)[10]，虽然是个 ( 数组 / 行 ) 指针，但并不是二重指针。这是因为传参时的隐式转化只能转化一层，因此一维数组传参时完全等价于 const 指针，但是二维数组就无法等价于二重指针。

另外 *var 确实代表 var[0] 这个数组，**var 也确实就是 var[0][0]，但是注意这里的 * 是运算符而不是类型定义。作为类型定义时，数组和指针是需要区分的。

B 中 var 的类型是指针数组，但是由于数组隐式转化的问题，其传参时表现出来的类型就是 char**，因此是正确的。

C 中 var 的类型是无类型指针，它可以指向任何东西。如果它指向的是一个 char*，那么它就符合 char** 的类型要求了，因此正确。

D 中 var 的类型是正统的 char**。
</details>
<br/>
P9.对于以下变量定义，正确的赋值是（）。

char *pc[5], s[10];
A.pc = s
B.*pc = s[0]
C.*pc = s
D.*pc = &s
<details>
<summary>answer & analysis</summary>
C.首先pc是一个指针数组，A显然错误。*pc相当于pc[0],B右边的s[0]是一个字符，不能给pc[0]（字符串）；D中&s是整个字符数组的地址，如果储存起来就是(char *)[10]，也不能赋给pc[0]；C中的s是字符数组，传递时隐式转换成char *，可以赋给pc[0].
</details>
<br/>

### Week11

Some points:
1.char *s = "Hello world!"中，s是一个指针，初始化为指向一个字符串常量，所以s实际上是const char *s，但由于历史原因编译器接受不带const的写法。（但是试图对s所指的字符串做写入会导致严重后果。）如果要修改字符串，则应写成数组char s[] = "Hello World!"。
<br/>
2.String Functions in the Standard Library
strlen:

    size_t strlen(const char *s)

return the length of a string('\0' not included)
<br/>
strcmp:

    int strcmp(const char *s1,const char *s2);
compare two strings,return:

    0 : s1 == s2
    >0 ：s1 > s2
    <0 : s1 < s2
<br/>
strcpy

    char *strcpy(char *restrict dst,const char *restrict stc);
把src的字符串拷贝到dst，restrict表明src和dst不重叠（C99），返回dst（链起代码）
<br/>
strcat

    char *strcat(char *restrict s1,const char *restrict s2);
把s2拷贝到s1后面，接成一个长字符串，返回s1。
<br/>
strchr/strrchr

    char *strchr(const char *s,int c);
    char *strrchr(const char *s,int c);
在字符串中找字符，返回NULL表示没有找到。
<br/>
strstr/strcasestr

    char *strstr(const char *s1,const char *s2);
    char *strcasestr(const char *s1,const char *s2);
在字符串中找字符串。
<br/>
<br/>
P1.不同类型的指针变量是可以直接相互赋值的。(T/F)
<details>
<summary>answer & analysis</summary>
F.会报错，一般需要强制转换。
但也有例外，如void*是可以直接赋值给其他指针的。
</details>
<br/>

P2.两个任意类型的指针可以使用关系运算符比较大小。(T/F)
<details>
<summary>answer & analysis</summary>
F.同类型的指针能用关系运算符比较大小，不同类型的指针则不能。
</details>
<br/>

P3.以下哪个定义中的p不是指针，请选择恰当的选项：

A.char **p;
B.char (*p)[10];
C.char *p[6];
D.给出的三项中，p都是指针
<details>
<summary>answer & analysis</summary>
C.char *p[6]是指针数组。
</details>
<br/>
P4.若有定义char *str[]={“Python”, “SQL”, “JAVA”, “PHP”, “C++”};则表达式*str[1] > *str[3]比较的是：

A.字符P和字符J
B.字符串SQL和字符串PHP
C.字符串Python和字符串JAVA
D.字符S和字符P
<details>
<summary>answer & analysis</summary>
D. 注意[]的优先级高于*，而str[1]指向"SQL"的首地址，解应用得到字符S，同理*str[3]得到字符P。
</details>
<br/>

<br/>

### Week14
1.在全局变量前加上static就使得它称为只能在所在编译单元中被使用的全局变量（静态变量）。类似地，在函数前面加上static就使得它成为只能在所在编译单元中被使用的函数（静态函数）。
<br/>
2.关于声明和定义：声明是不产生代码的东西，包括函数原型、变量声明、结构声明、宏声明、枚举声明、类型声明、inline函数等；而定义是产生代码的东西。下面是几个声明的例子：

    函数原型声明：int func(int a,int b);
    变量声明：extern int a;（声明一个整型全局变量）
    枚举声明：enum num｛one = 1,two,three｝;
<br/>
3.标准头文件结构：

    #ifndef __A_H__
    #define __A_H__
    ...
    #endif

运用条件编译宏，保证这个头文件在一个编译单元中只会被#include一次。
<br/>
4.前向声明：

    struct Node;
    typedef struct _list
    {
        Node *head;
        Node *tail;
    }
这里不需要具体知道Node是怎样的，所以可以用struct Node来告诉编译器Node是一个结构.
<br/>
<br/>

P1.静态局部变量如果没有赋值，其存储单元中将是随机值。(T/F)
<details>
<summary>answer & analysis</summary>
F. 静态局部变量如果没有显式初始化，会被程序自动初始化为0（对数值型变量）或空字符（对字符型变量）。
</details>
<br/>
P2.C语言中定义的静态变量存放在栈区，动态分配的内存空间位于堆区。(T/F)
<details>
<summary>answer & analysis</summary>
F. 常见的内存分区及存储内容：

>代码区：存放程序的代码（即CPU执行的机器指令），只读。
常量区：存放常量（如字符串字面量）。
静态区（全局区）：静态变量和全局变量的存储趋于是一起的，一旦静态区的内存被分配，静态区的内存知道程序全部结束之后才会被释放。
堆区：调用malloc函数申请的动态空间。
栈区：存放函数内的局部变量、形参和函数返回值。栈区里的数据作用范围过了之后，系统会回收自动管理栈区的内存。

</details>
P3.C语言的全局变量初始化是在以下哪个阶段完成的：

A.main()函数开始后
B.编译链接的时候
C.main()函数开始前
D.第一次用到的时候
<details>
<summary>answer & analysis</summary>
C. C语言的全局变量初始化是在main()函数开始前完成的。
</details>
<br/>
<br/>

### Week15
1.格式化的输入输出：
·printf
>%[flags][width][.prec][hIL]type

·scanf
>%[flag]type

flag|含义
-|:-:
-|左对齐
+|在前面放+或-
(space)|正数留空
0|0填充

<br/>

width或prec|含义
-|:-:
number|最小字符数
*|下一个参数是字符数
.number|小数点后的位数
.*|下一个参数是小数点后的位数

<br/>

类型修饰|含义
-|:-
hh|单个字节
h|short
l|long
ll|long long
L|long double

<br/>

type|用于|type|用于
-|:-|:-|:-
i或d|int|g|float
u|unsigned|G|float
o|八进制|a或A|十六进制浮点
x|十六进制|c|char
X|字母大写的十六进制|s|字符串
f或F|float，6|p|指针

<br/>

**scanf:%[flag]type**

flag|含义|flag|含义
-|:-|:-|:-
*|跳过|l|long,double
数字|最大字符数|ll|long long
hh|char|L|long double
h|short

scanf:%[flag]type

type|用于|type|用于
-|:-|:-|:-
d|int|s|字符串(单词)
i|整数，可能为十六进制或八进制|[...]|所允许的字符
u|unsigned int|p|指针
o|八进制|x|十六进制
a,e,f,g|float|c|char

注意printf和scanf的返回值：
·读入的项目数
·输出的字符数

2.file
>**·** FIlE *fopen(const char* restrict path,const char* restrict mode);
**·** int fclose(FILE* stream);
**·** fscanf(FILE*,...)
**·** fprintf(FILE*,..)

打开文件的标准代码：

    FILE *fp = fopen("file","r");
    if (fp)
    {
        fscanf(fp,...);
        fclose(fp);
    }
    else
    {
        ...
    }

#### fopen
指令|作用
-|:-
r|打开只读
r+|打开读写，从文件头开始
w|打开只写。如果不存在则新建，如果存在则清空
w+|打开读写。如果不存在则新建，如果存在则清空
a|打开追加。如果不存在则新建，如果存在则从文件尾开始
..x|只新建，如果文件已存在则不能打开

<br/>
P1.以下代码的输出为____.

    int x = -1;
    printf("%d",(unsigned int)x);

<details>
<summary>answer & analysis</summary>
-1. unsigned int的转换只是以无符号的方式来理解数据，并不会改变x的二进制值。对于printf来说，它要输出的是%d（有符号数），所以输出时仍当作有符号整型来理解。
</details>

<br/>
P2.以下代码的输出为_____.

     char str[100] = "ZhejiangU 1 3 5",s[10];
     int n;
     sscanf(str,"%s %*d %d %*d",s,&n);
     printf("%s",&s[n]);
<details>
<summary>answer & analysis</summary>
jiangU. %*d表示读取的是一个整型，但是直接忽略，不存到变量中。所以sscanf读取到的n是第二个数字3，然后输出s[3]开始的字符串，即jiangU.
</details>

## Resizable array
Definition:

    typedef struct
    {
        int *array;
        int size;
    }Array;
array_create:

    Array array_create(int init_size)
    {
        Array a;
        a.array = (int *)malloc(sizeof(int) * init_size);
        a.size = init_size;
        return a;
    }
array_free:

    void array_free(Array *a)
    {
        free(a->array);
        a->array = NULL;
        a->size = 0;
    }
array_size:

    int array_size(const Array *a)
    {
        return a->size;
    }
array_at(the first index is 0):

    int *array_at(Array *a,int index)
    {
        if (index >= a->size)
        {
            array_inflate(a,index - a->size);
        }
        return &(a->array[index]);
    }
array_inflate

    void array_inflate(Array *a,int more_size)
    {
        int *p = (int *)malloc(sizeof(int) * (a->size + more_size));
        for (int i=0;i<a->size;i++) p[i] = a->array[i];
          //or:memcpy((void *)p,(void *)a->array,a->size*sizeof(int));
        free(a->array); 
        a->array = p;
        a->size = a->size + more_size;
    }
<br/>

## Linked Array
Definition:

    typedef struct _array
    {
        int *array;
        int size;
        struct _array *next;
    }Array;
array_create:

    Array array_create()
    {
        Array a;
        a.array = (int *)malloc(sizeof(int) * BLOCK_SIZE);
        a.size = BLOCK_SIZE;
        a.next = 0;
        return a;
    }
array_free:

    void array_free(Array *a)
    {
        free(a->array);
        a->size = 0;
        if (a->next)
        {
            array_free(a->next);
            free(a->next);
        }
    }
array_size:

    int array_size(Array *a)
    {
        if (a->next == NULL)
        {
            return a->size;
        }
        else
        {
            return a->size + array_size(a->next);
        }
    }
array_at:

    int *array_at(Array *a,int index)
    {
        if (index < a->size)
        {
            return &(a->array[index]);
        }
        else
        {
            return array_at(a->next,index - a->size);
        }
    }
array_inflate:

    void array_inflate(Array *a)
    {
        Array new_array;
        new_array->array = (int *)malloc(sizeof(int) * BLOCK_SIZE);
        new_array->size = BLOCK_SIZE;
        new_array->next = 0;
        for (Array pre = a;pre->next;pre = pre->next) ;
        pre->next = &new_array;
    }
<br/>

## Linked List
defintion:

    typedef struct _node
    {
        int value;
        struct _node *next;
        struct _node *prev;
    }Node;
    typedef struct
    {
        Node *head;
        Node *tail;
    }List;
list_create:

    List *list_create()
    {
        List *list = malloc(sizeof(List));
        list->head = NULL;
        list->tail = NULL;
        return list;
    }
insert_head:

    void insert_head(List *list,int value)
    {
        Node *node = malloc(sizeof(Node));
        node->value = val;
        node->prev = NULL;
        if (list->head)
        {
            node->next = list->head;
            list->head->prev = node;
            list->head = node;
        }
        else
        {
            node->next = node->prev = NULL;
            list->head = list->tail = node;
        }
    }
append_tail:

    void append_tail(List *list,int val)
    {
        Node *node = malloc(sizeof(Node));
        node->value = val;
        node->next = NULL;
        if (list->tail)
        {
            node->prev = list->tail;
            list->tail->next = node;
            list->tail = node;
        }
        else
        {
            node->prev = NULL;
            list->head = list->tail = node;
        }
    }
insert_middle:

    void insert_middle(List *list,int index,int val)
    {
        int cnt = 1;
        Node *p = list->head;
        for (;cnt<index && p;p = p->next,cnt++) ;
        Node *node = malloc(sizeof(Node));
        node->value = val;
        node->prev = p;
        node->next = p->next;
        p->next->prev = node;
        p->next = node;
    }
remove:

    void remove_node(List *list,int val)
    {
        Node *p = list->head;
        for (;p;)
        {
            if (p->value == val)
            {
                if (list->head == p)
                {
                    list->head = p->next;
                    if (list->tail == p)
                    {
                        list->tail = NULL;
                    }
                    Node *tmp = p;
                    p = p->next;
                    free(tmp);
                }
                else if (list->tail == p)
                {
                    list->tail = p->prev;
                    p->prev->next = NULL;
                    free(p);
                    break;
                }
                else
                {
                    p->prev->next = p->next;
                    p->next->prev = p->prev;
                    Node *tmp = p;
                    p = p->next;
                    free(tmp);
                }
            }
            else p = p->next;
        }
    }
traversal:

    void traversal(List *list)
    {
        for (Node *p = list->head;p;p = p->next)
            ...
    }
search:

    int search(List *list,int val)
    {
        int index = 1;
        for (Node *p = list->head;p;p = p->next,index++)
            if (p->value == val)
            {
                return index;
            }
        return -1;
    }
free:

    void list_free(List *list)
    {
        for (Node *p = list->head;p;)
        {
            Node *tmp = p;
            p = p->next;
            free(tmp);
        }
        list->head = list->tail = NULL;
        free(list);
    }

<br/>
<br/>

### 杂项
1.关于字符串长度：字符串中出现\ddd时可能为八进制转义字符，取决于后续是否为合法的八进制，以\开始，最少1位，最多3位。此外应注意strlen和sizeof的区别。
examples:

    char str[] = "hello\61234";
    printf("%s\n",str);
    printf("%d %d\n",strlen(str),sizeof(str));

    output:
    hello1234
    9 10



    char str[] = "123\029\08";
    printf("%d %d\n,strlen(str),sizeof(str));

    output:5 8
<br/>

2.关于sizeof问题：
>（1）sizeof是C语言中的一个运算符（而非函数！），它的作用是查询占据的空间字节数。
常见的类型及其所占的字节数:
(unsigned)char(1 Byte),
(unsigned) short(2 Byte),
(unsigned) int(4 Byte(64bit)),
(unsigned) long(4 Byte),
(unsigned) long long(8 Byte),
float(4 Byte),long double(16 Byte(64bit)),
pointer(8 Byte(64bit)).
（2）sizeof后的操作数可以是一个表达式或者括在括号里的类型名，且会忽略括号里的各种运算。
（3）sizeof的两种用法：
sizeof unary-expression
sizeof (type-name)

An example:

    char ch = 'a';
    printf("%lu\n",sizeof(ch));
    printf("%lu\n",sizeof(ch + 1));
    printf("%lu\n",sizeof('a'));

    output:
    1
    4
    4 ('a'是字符常量，被看成int类型)

<br/>

3.关于运算符",":逗号运算符会顺序执行一系列运算。整个逗号表达式的值是以逗号分隔的列表中最后一个表达式的值。
<br/>

4.相同类型的指针相减结果为两指针之间差了多少单位距离，而不是指针的值相减。下面是一个例子：

    int a[] = {1,2,3,4,5};
    int *p = a,*q = &a[2];
    printf("%lu\n",q - p);
    printf("%d\n",(int)&a[2] - (int)a);

    
    output:
    2
    8


### About operator precedence

优先级|运算符|结合性/目数
-|:-:|-:
1|[]数组 ()|/
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

单目>双目
<br/>

#### About escape char
char|meaning
-|:-:
\b|back position
\t|next table stop
\\"|double quote
\\'|single quote
\n|new line
\r|return the carriage

<br/>

### Some Common C Keywords

auto 
bool(C23)
break
case
char
const
continue
default
do
double
else
enum
extern
false(C23)
float
for
goto
if
inline
int
long
register
return
short
signed
sizeof
static
sturct
switch
true(C23)
typedef
union
unsigned
void
while

Pay attention:define and include are not keywords!



<br/>
<br/>
<br/>
<br/>


#### translation:
adjacent相邻的
argument参数（实参？）
assignment operator（赋值运算符）
binary二进制
capital大写字母
coefficient系数
convert转换
decimal十进制
exponent指数
hexadecimal十六进制
mechanism机制
octal八进制
parameter参数（形参？）
polynomial（多项式）
prototype原型
recursion递归
scope范围
string literal字符串字面量
sub expression子表达式
unary operator单目运算符





<br/>
<br/>




#### *several tiny points:*


