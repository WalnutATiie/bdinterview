**（1） 多态性都有哪些？**

- 1.参数多态 包括函数模板和类模板,模板属于编译时多态，编译时根据模板生成模板函数。
- 2.包含多态  virtual
- 3.重载多态  重载多态是指函数名相同，但函数的参数个数或者类型不同的函数构成多态
- 4.强制多态  强制类型转换

（2） 动态绑定怎么实现?

**（3） 类型转换有哪些？（四种类型转换，分别举例说明）**

> 强制类型转换：在一个类型前面加( )，来强制转换

long l = 9L;
int i = (int)l;

> 自动类型转换：

int i = 5;
String str = “”+i;
> 向上造型：把范围小的造型为范围大的类型： int i = 2;

long l = i;


**（4） 操作符重载（+操作符），具体如何去定义，？**

new、delete、=、[]、-> 等只能作为类的成员函数重载

重载为类成员函数时参数个数=原操作数个数-1（后置++、--除外）
重载为友元函数时 参数个数=原操作数个数，且至少应该有一个自定义类型的形参

**（5） 内存对齐的原则？（原则叙述了一下并举例说明）**

- 字符类型占1字节， 可以从任何地址开始
- short类型占2字节， 必须从2字节倍数地址开始
- int类型占4字节，必须从4字节倍数地址开始
- Union结构体，sizeof的取值不仅考虑sizeof最大的成员，还要考虑对齐字节，对齐字节的取值是取成员类型字节最大值与指定对齐字节

结构体的总大小,也就是sizeof的结果,.必须是其内部最大成员的"最宽基本类型成员"的整数倍.不足的要补齐

**（6） 模版怎么实现？**

- 函数模板的实例化是由编译程序在处理函数调用时自动完成的
- 类模板的实例化必须由程序员在程序中显式地指定
- 函数模板针对仅参数类型不同的函数
- 类模板针对仅数据成员和成员函数类型不同的类

（7） 指针和const的用法？



**（8） 虚函数、纯虚函数、虚函数与析构函数？（纯虚函数如何定义，为什么析构函数要定义成虚函数）**
> 
>   不能被声明为虚函数的是：

- 1.普通函数（不能被覆盖） 
- 2.友元函数（C++不支持友元函数继承）
- 3.内联函数（编译期间展开，虚函数是在运行期间绑定）
- 4.构造函数（没有对象不能使用构造函数，先有构造函数后有虚函数，虚函数是对对象的动作） 
- 5.静态成员函数（只有一份大家共享） 


> 构造函数不能声明为虚函数的原因是: 

- 1 构造一个对象的时候，必须知道对象的实际类型，而虚函数行为是在运行期间确定实际类型的。而在构造一个对象时，由于对象还未构造成功。编译器无法知道对象 的实际类型，是该类本身，还是该类的一个派生类，或是更深层次的派生类。无法确定。。。
- 2 虚函数的执行依赖于虚函数表。而虚函数表在构造函数中进行初始化工作，即初始化vptr，让他指向正确的虚函数表。而在构造对象期间，虚函数表还没有被初 始化，将无法进行。

**（9） 内联函数（内联函数的优点以及和宏定义的区别）**

宏只是预定义的函数，在编译阶段不进行类型安全性检查，在编译的时候将对应函数用宏命令替换。对程序性能无影响

> 内联函数：

Tip： 只有当函数只有 10 行甚至更少时才将其定义为内联函数.
定义: 当函数被声明为内联函数之后, 编译器会将其内联展开, 而不是按通常的函数调用机制进行调用.
 一个较为合理的经验准则是, 不要内联超过 10 行的函数. 谨慎对待析构函数, 析构函数往往比其表面看起来要更长, 因为有隐含的成员和基类析构函数被调用!<br/>
 内联那些包含循环或 switch 语句的函数常常是得不偿失 (除非在大多数情况下, 这些循环或 switch 语句从不被执行).<br/>
有些函数即使声明为内联的也不一定会被编译器内联, 这点很重要; 比如虚函数和递归函数就不会被正常内联. 通常, 递归函数不应该声明成内联函数.(递归调用堆栈的展开并不像循环那么简单, 比如递归层数在编译时可能是未知的, 大多数编译器都不支持内联递归函数)<br/>

内联函数是使用inline关键字声明的函数，也成内嵌函数，它主要的作用是解决程序的运行效率。
使用内联函数的时候要注意：

- 1.递归函数不能定义为内联函数
- 2.内联函数一般适合于不存在while和switch等复杂的结构且只有1~5条语句的小函数上，否则编译系统将该函数视为普通函数。
- 3.内联函数只能先定义后使用，否则编译系统也会把它认为是普通函数。
- 4.对内联函数不能进行异常的接口声明。



**（10） const和typedef(const的用处，有那些优点）**

- 1) #define是预处理指令，在编译预处理时进行简单的替换，不作正确性检查，不关含义是否正确照样带入，只有在编译已被展开的源程序时才会发现可能的错误并报错。例如：

 #define PI 3.1415926
 程序中的：area=PI*r*r 会替换为3.1415926*r*r
如果你把#define语句中的数字9 写成字母g 预处理也照样带入。
 
- 2）typedef是在编译时处理的。它在自己的作用域内给一个已经存在的类型一个别名，但是You cannot use the typedef specifier inside a function definition。

- 3）
    typedef int * int_ptr;
与`#define int_ptr int * `

作用都是用int_ptr代表 int * ,但是二者不同，正如前面所说 ，#define在预处理 时进行简单的替换，而typedef不是简单替换 ，而是采用如同定义变量的方法那样来声明一种类型。也就是说;

- #define int_ptr int *
- int_ptr a, b; //相当于int * a, b; 只是简单的宏替换

- typedef int* int_ptr;
- int_ptr a, b; //a, b 都为指向int的指针,typedef为int* 引入了一个新的助记符

**define和const的区别**

本质：define只是字符串替换，const参与编译运行，具体的： 
• define不会做类型检查，const拥有类型，会执行相应的类型检查 
• define仅仅是宏替换，不占⽤用内存，⽽而const会占用内存 
• const内存效率更高，编译器通常将const变量保存在符号表中，而不会分配存储空间，这使得它成 为一个编译期间的常量，没有存储和读取的操作

（11） 排序算法有哪些？快速排序怎么实现的？最好时间复杂度，平均时间复杂度

**（12） 链接指示：extern “C”（作用）**

extern "C" 包含双重含义，从字面上即可得到：首先，被它修饰的目标是“extern”的；其次，被它修饰的目标是“C”的。 

- （1） 被extern "C"限定的函数或变量是extern类型的 
 extern是C/C++语言中表明函数和全局变量作用范围（可见性）的关键字，该关键字告诉编译器，其声明的函数和变量可以在本模块或其它模块中使用。记住，下列语句： 
extern int a; <br/>
 仅仅是一个变量的声明，其并不是在定义变量a，并未为a分配内存空间。变量a在所有模块中作为一种全局变量只能被定义一次，否则会出现连接错误。 <br/>
通常，在模块的头文件中对本模块提供给其它模块引用的函数和全局变量以关键字extern声明。例如，如果模块B欲引用该模块A中定义的全局变量和函数时只需包含模块A的头文件即可。这样，模块B中调用模块A中的函数时，在编译阶段，模块B虽然找不到该函数，但是并不会报错；它会在连接阶段中从模块A编译生成的目标代码中找到此函数。 <br/>
与extern对应的关键字是static，被它修饰的全局变量和函数只能在本模块中使用。因此，一个函数或变量只可能被本模块使用时，其不可能被extern “C”修饰。 <br/>
- （2） 被extern "C"修饰的变量和函数是按照C语言方式编译和连接的<br/>

（13） c语言和c++有什么区别？（大体讲了 一下，继承、多态、封装、异常处理等）

（14）strcpy函数的编写？

    如果编写一个标准strcpy函数的总分值为10，下面给出几个不同得分的答案：   
    2分 

    void strcpy( char *strDest, char *strSrc )
    {
      while( (*strDest++ = * strSrc++) != ‘\0’ );
    }
    4分   

    void strcpy( char *strDest, const char *strSrc ) 
    //将源字符串加const，表明其为输入参数，加2分
    {
      while( (*strDest++ = * strSrc++) != ‘\0’ );
    }
    7分   

    void strcpy(char *strDest, const char *strSrc) 
    {
     //对源地址和目的地址加非0断言，加3分
     assert( (strDest != NULL) && (strSrc != NULL) );
     while( (*strDest++ = * strSrc++) != ‘\0’ );
    }
    10分   
    //为了实现链式操作，将目的地址返回，加3分！   
    char * strcpy( char *strDest, const char *strSrc ) 
    {
     assert( (strDest != NULL) && (strSrc != NULL) );
     char *address = strDest; 
     while( (*strDest++ = * strSrc++) != ‘\0’ ); 
     return address;
	}


**（17） new与malloc的区别，delet和free的区别？**

malloc，calloc，realloc，free属于C函数库，而new/delete则是C++函数库；<br/>

new 不止是分配内存，而且会调用类的构造函数，同理delete会调用类的析构函数，而malloc则只分配内存，不会进行初始化类成员的工作，同样free也不会调用析构函数<br/>
基本类型的对象没有析构函数，所以回收基本类型组成的数组空间用 delete 和 delete[] 都是应该可以的；但是对于类对象数组，只能用 delete[]。

其他：
1. malloc，calloc，realloc，free属于C函数库，而new/delete则是C++函数库；
2. 多个-alloc的比较：
    alloc：唯一在栈上申请内存的，无需释放；
    malloc：在堆上申请内存，最常用；
    calloc：malloc+初始化为0；
    realloc：将原本申请的内存区域扩容，参数size大小即为扩容后大小，因此此函数要求size大小必须大于ptr内存大小。


（18） 为什么要用static_cast转换而不用c语言中的转换？

（19） 异常机制是怎么回事？

**（20） 迭代器删除元素的会发生什么？**

- 1. 对于关联容器(如map, set, multimap,multiset)，删除当前的iterator，仅仅会使当前的iterator失效，只要在erase时，递增当前iterator即可。这是因为map之类的容器，使用了红黑树来实现，插入、删除一个结点不会对其他结点造成影响。
- 2.  对于序列式容器(如vector,deque)，删除当前的iterator会使后面所有元素的iterator都失效。这是因为vetor,deque使用了连续分配的内存，删除一个元素导致后面所有的元素会向前移动一个位置。还好erase方法可以返回下一个有效的iterator。
- 3.  对于list来说，它使用了不连续分配的内存，并且它的erase方法也会返回下一个有效的iterator，因此上面两种方法都可以使用。


**（21） 必须在构造函数初始化式里进行初始化的数据成员有哪些？**

常量成员和引用成员自然是要初始化的，问题就在这static成员。<br/>
static成员是不允许在类内初始化的，除了const，那么static const 成员是不是在初始化列表中呢？<br/>
答案是NO<br/>
一是static属于类，它在未实例化的时候就已经存在了，而构造函数的初始化列表嘞，只有在实例化的时候才执行。<br/>
二是static成员不属于对象。我们在调用构造函数自然是创建对象，一个跟对象没直接关系的成员要它做什么呢<br/>

（23） auto_ptr类：

（24） 继承机制中对象之间是如何转换的？

（25）虚函数，虚函数表里面内存如何分配？

（26）如何实现只能动态分配类对象，不能定义类对象？（这个牛客上的题目，我把如何只能动态分配和只能静态分配都讲了一下）

（27） stl有哪些容器，对比vector和set？

 28） 红黑树的定义和解释？

**（29） const关键字的作用？（const成员函数，函数传递，和define的区别）**

- 1. 不能在const函数中修改所在类的对象的数据，因为const函数中的*this是常量，同样只能访问const函数；
- 2. const函数中只能调用其他的const函数，不能调用非const函数，因为对象调用函数是需要传递对象自己，const函数中的*this是常量，非const函数中的*this是变量，因此不可以调用(除非去除*this的const属性)；
- Note:使用const_cast后，可以在const函数中调用非const函数的
- 3. const函数与同名的非const函数是重载函数；
- 4. const对象只能调用const函数 ，但是非const对象可以调用const函数。
coust是常对象，也就是不改变成员变量的值，而成员函数中只有const函数可以确保不改变成员变量的值

（30） 静态成员函数和数据成员有什么意义？

（31） 模版特化的概念，为什么特化？

（32） explicit是干什么用的？

（33） strcpy返回类型是干嘛用的？

 **（34）拷贝构造函数**

- 1. 在声明语句中用一个对象初始化另一个对象；
- 2. 将一个对象作为参数按值调用方式传递给另一个对象时生成对象副本；
- 3. 生成一个临时对象作为函数的返回结果。

**(35)STL容器**

vector，erase(pos)，直接把pos+1到finish的数据拷贝到以pos为起点的区间上，也就是vector的长度会逐渐变短，同时iter会逐渐往后移动，直到iter == cont.end()，由于容器中end()返回的迭代器是最后一个元素的下一个（这个地方没有任何值），现在考虑这个状态前一个状态，此时要删除的点是iter, tempIt = iter, ++iter会指向此时的end()，但是执行erase(tempIt)之后，end()向前移动了！！！问题来了，此时iter空了！！！不崩溃才怪。


vector:随机访问迭代器,复杂度O（1）<br/>
deque：同上，O（1）<br/>
map：双向迭代器，不过由于是关联容器，需要通过key访问alue的方法，O（h），h为树的高度<br/>
unordered_map：前向迭代器，同上，平摊复杂度O（1），最差O（n），也与散列函数的好坏有关。<br/>
string：同vector<br/>
只有dqeue和vector是连续存储的


**(36)进程间通信**

- Linux进程间通信：管道、信号、消息队列、共享内存、信号量、套接字(socket)
- Linux线程间通信：互斥量（mutex），信号量，条件变量
- Windows进程间通信：管道、消息队列、共享内存、信号量   （semaphore）   、套接字(socket)
- Windows线程间通信：互斥量（mutex），信号量（semaphore）、临界区（critical section）、事件（event）

**(37)内存四区**

- a 全局变量 存放在全局变量区
- b 类的成员变量 由类的定义决定  在main函数中类A动态分配 因此b在堆区
- c 静态成员 静态存储区
- d 局部变量 栈区

**（38）引用和指针**

- 1. 指针是一个实体，而引用仅是个别名；
- 2. 引用使用时无需解引用(*)，指针需要解引用；
- 3. 引用只能在定义时被初始化一次，之后不可变；指针可变；
- 4. 引用没有 const，指针有 const；
- 5. 引用不能为空，指针可以为空；
- 6. “sizeof 引用”得到的是所指向的变量(对象)的大小，而“sizeof 指针”得到的是指针本身(所指向的变量或对象的地址)的大小；
- 7. 指针和引用的自增(++)运算意义不一样；
- 8.从内存分配上看：程序为指针变量分配内存区域，而引用不需要分配内存区域。

**（39）c++中的类和c中的struct**

- 在C++中，来自class的继承默认按照private继承处理，来自struct的继承默认按照public继承处理
- c里面的struct只是变量的聚合体，struct不能有函数

**（40）接口和抽象类**

- 1、一个子类只能继承一个抽象类（虚类），但能实现多个接口；
- 2、一个抽象类可以有构造方法，接口没有构造方法；
- 3、一个抽象类中的方法不一定是抽象方法，即其中的方法可以有实现（有方法体），接口中的方法都是抽象方法，不能有方法体，只有声明；
- 4、一个抽象类可以是public、private、protected、default,
   接口只有public;
- 5、一个抽象类中的方法可以是public、private、protected、default，
   接口中的方法只能是public和default

**（41）static和const的作用**

**static关键字至少有下列n个作用：** 

- （1）函数体内static变量的作用范围为该函数体，不同于auto变量，该变量的内存只被分配一次，因此其值在下次调用时仍维持上次的值；   
- （2）在模块内的static全局变量可以被模块内所用函数访问，但不能被模块外其它函数访问；   
- （3）在模块内的static函数只可被这一模块内的其它函数调用，这个函数的使用范围被限制在声明它的模块内；   
- （4）在类中的static成员变量属于整个类所拥有，对类的所有对象只有一份拷贝；   
- （5）在类中的static成员函数属于整个类所拥有，这个函数不接收this指针，因而只能访问类的static成员变量。    

**const关键字至少有下列n个作用**   

- （1）欲阻止一个变量被改变，可以使用const关键字。在定义该const变量时，通常需要对它进行初始化，因为以后就没有机会再去改变它了；   
- （2）对指针来说，可以指定指针本身为const，也可以指定指针所指的数据为const，或二者同时指定为const；   
- （3）在一个函数声明中，const可以修饰形参，表明它是一个输入参数，在函数内部不能改变其值；   
- （4）对于类的成员函数，若指定其为const类型，则表明其是一个常函数，不能修改类的 成员变量；   
- （5）对于类的成员函数，有时候必须指定其返回值为const类型，以使得其返回值不为“左值”。例如：   
`const classA operator*(const classA& a1,const classA& a2);  `   <br/>

operator*的返回结果必须是一个const对象。如果不是，这样的变态代码也不会编译出错：   <br/>
  
    classA a, b, c;   
    (a * b) = c; // 对a*b的结果赋值 

**（42）类成员函数的重载、覆盖和隐藏区别？**<br/>

 a.成员函数被重载的特征：

- （1）相同的范围（在同一个类中）；
- （2）函数名字相同；
- （3）参数不同；
- （4）virtual 关键字可有可无。

 b.覆盖是指派生类函数覆盖基类函数，特征是：

- （1）不同的范围（分别位于派生类与基类）；
- （2）函数名字相同；
- （3）参数相同；
- （4）基类函数必须有virtual 关键字

c.“隐藏”是指派生类的函数屏蔽了与其同名的基类函数，规则如下：

- （1）如果派生类的函数与基类的函数同名，但是参数不同。此时，不论有无virtual关键字，基类的函数将被隐藏（注意别与重载混淆）。
- （2）如果派生类的函数与基类的函数同名，并且参数也相同，但是基类函数没有virtual 关键字。此时，基类的函数被隐藏（注意别与覆盖混淆）

**(43).sizeof 和 strlen的区别：**

- sizeof 是一个操作符，而 strlen 是库函数。

- sizeof 的参数可以是数据类型，可以是变量，而 strlen 的参数只能是以 '\0' 结尾的字符串。

- 编译器在编译时就计算出了 sizeof 的大小，而 strlen 要在运行后才能计算出大小。

- sizeof 计算的是类型所占内存的字节数，而 strlen 计算的是字符串的有效长度。

- 数组做 sizeof 的参数不会退化，而数组做 strlen 的参数会退化成指针

**(44)指针和数组的区别**

（ 1 ）数组要么在全局数据区被创建，要么在栈上被创建；指针可以随时指向任意类型的内存块；

（ 2 ）修改内容上的差别：

char a[] = “hello”;
a[0] = ‘X’;
char *p = “world”; // 注意 p 指向常量字符串 
p[0] = ‘X’; // 编译器不能发现该错误，运行时错误

(3) 用运算符 sizeof 可以计算出数组的容量（字节数）。 sizeof(p),p 为指针得到的是一个指针变量的字节数，而不是 p 所指的内存容量。 C++/C 语言没有办法知道指针所指的内存容量，除非在申请内存时记住它。注意当数组作为函数的参数进行传递时，该数组自动退化为同类型的指针。


**(45)继承机制**

- 1.继承机制中对象之间是如何转换的？
- 2.继承机制中引用和指针之间如何转换？
- 3.继承机制中父类指针转换为子类指针发生了什么？
- 4.继承机制中子类指针转换为父类指针发生了什么？

当派生类以public方式继承基类时, 编译器可以自动将派生类对象指针或引用转化成基类对象指针或引用。 派生类对象自动转化成基类对象时会造成派生类对象特有成员丢失。

当派生类以private/protected方式继承基类时, 派生类对象指针或引用转化成基类对象指针或引用需要强制类型转化, 但不能用static_cast 要用reinterpret_cast, 不能把派生类对象强制转换成基类对象。

基类对象指针或引用可以强制类型转换成派生类对象指针或引用, 而基类对象无法转化成派生类对象。
向下转型不安全, 没有自动转换的机制。


**(46)C++  和  Java  最大的区别是什么**

**(47)10个C++11特性**

**auto**:在 C++11 之前， auto 关键字用来指定存储期。在新标准中，它的功能变为类型推断。 auto 现在成了一个类型的占位符，通知编译器去根据初始化代码推断所声明变量的真实类型。各种作用域内声明变量都可以用到它<br/>
**nullptr**:以前都是用 0 来表示空指针的，但由于 0 可以被隐式类型转换为整形，这就会存在一些问题。关键字 nullptr 是 std::nullptr_t 类型的值，用来指代空指针。 nullptr 和任何指针类型以及类成员指针类型的空值之间可以发生隐式类型转换，同样也可以隐式转换为 bool 型（取值为 false ）。但是不存在到整形的隐式类型转换。

**(48)C++各种智能指针**

auto_ptr、unique_ptr和shared_ptr这几个智能指针背后的设计思想。我简单的总结下就是：将基本类型指针封装为类对象指针（这个类肯定是个模板，以适应不同基本类型的需求），并在析构函数里编写delete语句删除指针指向的内存空间。<br/>

不能自动将指针转换为智能指针对象，必须显式调用<br/>

    shared_ptr<double> pd; 
    double *p_reg = new double;
    pd = p_reg;   // not allowed (implicit conversion)
    pd = shared_ptr<double>(p_reg);   // allowed (explicit conversion)
    shared_ptr<double> pshared = p_reg;   // not allowed (implicit conversion)
    shared_ptr<double> pshared(p_reg);// allowed (explicit conversion)

（1）如果程序要使用多个指向同一个对象的指针，应选择shared_ptr。这样的情况包括：

有一个指针数组，并使用一些辅助指针来标示特定的元素，如最大的元素和最小的元素；<br/>

两个对象包含都指向第三个对象的指针；<br/>

STL容器包含指针。很多STL算法都支持复制和赋值操作，这些操作可用于shared_ptr，但不能用于unique_ptr（编译器发出warning）和auto_ptr（行为不确定）。如果你的编译器没有提供shared_ptr，可使用Boost库提供的shared_ptr。<br/>

（2）如果程序不需要多个指向同一个对象的指针，则可使用unique_ptr。如果函数使用new分配内存
，并返还指向该内存的指针，将其返回类型声明为unique_ptr是不错的选择。<br/>
这样，所有权转让给接受返回值的unique_ptr，而该智能指针将负责调用delete。可将unique_ptr存储到STL容器在那个，只要不调用将一个unique_ptr复制或赋给另一个算法（如sort()）<br/>

**重载**

c++不能重载的运算符有.（点号），::（域解析符），?:（条件语句运算符），sizeof（求字节运算符），typeid，static_cast，dynamic_cast，interpret_cast（三类类型转换符）

**深拷贝和浅拷贝：**

在有指针的情况下，浅拷贝只是增加了一个指针指向已经存在的内存，而深拷贝就是增加一个指针并且申请一个新的内存，使这个增加的指针指向这个新的内存，采用深拷贝的情况下，释放内存的时候就不会出现在浅拷贝时重复释放同一内存的错误！

指针数组如果没有初始化则任意指向，不会调用构造函数。MyClass a[4]，*p[5]；
语句时会自动调用该类构造函数的次数是4

**内存对齐原则**：

一、结构体变量的首地址能够被其最宽基本类型成员大小与对齐基数中的较小者所整除；
二、结构体每个成员相对于结构体首地址的偏移量(offset)都是该成员大小与对齐基数中的较小者的整数倍，如有需要编译器会在成员之间加上填充字节(internal adding)；
三、结构体的总大小为结构体最宽基本类型成员大小与对齐基数中的较小者的整数倍，如有需要编译器会在最末一个成员之后加上填充字节(trailing padding)。

```
对齐原则：每一成员需对齐为后一成员类型的倍数
补齐原则：最终大小补齐为成员类型最大值的倍数
structA
{
 inta;     // 4
 shortb;   // (4) + 2 = 6 下一元素为 int，需对齐为 4 的倍数， 6 + (2) = 8
 intc;     // (8) + 4 = (12)
 chard;    // (12) + 1 = 13， 需补齐为 4 的倍数，13 + (3) = 16
};
structB
{
 inta;     // 4
 shortb;   // (4) + 2 = 6，下一成员为 char 类型，不考虑对齐
 charc;    // (6) + 1 = 7，下一成员为 int 类型，需对其为 4 的倍数，7 + (1) = 8
 intd;     // (8) + 4 = 12，已是 4 的倍数
}
```


类指针的声明不会调用构造函数，但指向一个类实例会调用构造函数。类的声明也会调用构造函数。


在析构和构造函数中调用类自己的虚函数，虚函数的动态绑定机制不会生效，由于类的构造次序是由基类到派生类，所以在构造函数中调用虚函数，这个虚函数不会呈现出多态； 相反，类的析构是从派生类到基类，当调用继承层次中某一层次的类的析构函数时往往意味着其派生类部分已经析构掉，所以也不会呈现出多态

**C++ STL 的实现**：
- 1.vector  底层数据结构为数组 ，支持快速随机访问
- 2.list    底层数据结构为双向链表，支持快速增删
- 3.deque   底层数据结构为一个中央控制器和多个缓冲区，详细见STL源码剖析P146，支持首尾（中间不能）快速增删，也支持随机访问
- 4.stack   底层一般用23实现，封闭头部即可，不用vector的原因应该是容量大小有限制，扩容耗时
- 5.queue   底层一般用23实现，封闭头部即可，不用vector的原因应该是容量大小有限制，扩容耗时
- 6.45是适配器,而不叫容器，因为是对容器的再封装
- 7.priority_queue 的底层数据结构一般为vector为底层容器，堆heap为处理规则来管理底层容器实现
- 8.set       底层数据结构为红黑树，有序，不重复
- 9.multiset  底层数据结构为红黑树，有序，可重复 
- 10.map      ﻿﻿﻿﻿底层数据结构为红黑树，有序，不重复
- 11.multimap 底层数据结构为红黑树，有序，可重复
- 12.hash_set ﻿﻿﻿﻿底层数据结构为hash表，无序，不重复
- 13.hash_multiset 底层数据结构为hash表，无序，可重复 
- 14.hash_map      ﻿﻿﻿﻿底层数据结构为hash表，无序，不重复
- 15.hash_multimap 底层数据结构为hash表，无序，可重复 

- int(*n)[10]; 是数组指针  sizeof(n)=4
- int* n[10];  是指针数组  sizeof(n)=40
- 


```
函数模板的格式：
template <class 形参名，class 形参名，......> 返回类型 函数名(参数列表)
{
函数体
}

类模板的格式为：
template<class   形参名 ，class 形参名，…>   class 类名
{ ... };
```

inline函数中如果有局部变量，同时，传参给inline函数时使用表达式传参，这样，编译器在处理时会产生很多临时对象，当inline函数多次被调用时，会产生大量的扩展码，从而增加程序大小；
如果inline函数被编译器接受，同时又没有产生以上这些副作用，那么同非内联函数相比，inline函数是用函数体直接替换，省去了函数调用的开销，加快程序执行速度

运算符重载时要遵循一个规则，即 除了类属关系运算符"."、成员指针运算符".*"、作用域运算符"::"、sizeof运算符和三目运算符"?:"以外，C++中的所有运算符都可以重载。


当free释放内存之后，指针还指向原来的那块地址，需要我们设置 p = NULL；如果不手动设置 p = NULL，此时P就变成了野指针

clone是fork的升级版本，不仅可以创建进程或者线程，还可以指定创建新的命名空间（namespace）、有选择的继承父进程的内存、甚至可以将创建出来的进程变成父进程的兄弟进程等等


sizeof（指针）只能返回指针本身占用的字节数而不能确定为它指向的内容分配的空间的大小。


**动态和静态链接库**

1 静态链接库的优点 

-  (1) 代码装载速度快，执行速度略比动态链接库快； 
-  (2) 只需保证在开发者的计算机中有正确的.LIB文件，在以二进制形式发布程序时不需考虑在用户的计算机上.LIB文件是否存在及版本问题，可避免DLL地狱等问题。 
 
2 动态链接库的优点 

-  (1) 更加节省内存并减少页面交换；
-  (2) DLL文件与EXE文件独立，只要输出接口不变（即名称、参数、返回值类型和调用约定不变），更换DLL文件不会对EXE文件造成任何影响，因而极大地提高了可维护性和可扩展性；
-  (3) 不同编程语言编写的程序只要按照函数调用约定就可以调用同一个DLL函数；
-  (4)适用于大规模的软件开发，使开发过程独立、耦合度小，便于不同开发者和开发组织之间进行开发和测试。

3 不足之处

-  (1) 使用静态链接生成的可执行文件体积较大，包含相同的公共代码，造成浪费；
-  (2) 使用动态链接库的应用程序不是自完备的，它依赖的DLL模块也要存在，如果使用载入时动态链接，程序启动时发现DLL不存在，系统将终止程序并给出错误信息。而使用运行时动态链接，系统不会终止，但由于DLL中的导出函数不可用，程序会加载失败；速度比静态链接慢。当某个模块更新后，如果新模块与旧的模块不兼容，那么那些需要该模块才能运行的软件，统统撕掉。这在早期Windows中很常见。


赋值运算符重载函数 ” 不是不能被派生类继承，而是被派生类的默认 “ 赋值运算符重载函数 ” 给覆盖了。 

这就是 C++ 赋值运算符重载函数不能被派生类继承的真实原因！ “

**模板类**

- (1)可用来创建动态增长和减小的数据结构，标准库容器支持模板 可以认为容器就是动态增长和减小的数据结构
- （2）它是类型无关的，因此具有很高的可复用性。
- （3）它在编译时而不是运行时检查数据类型，保证了类型安全
- （4）它是平台无关的，可移植性
- （5）可用于基本数据类型



**类型兼容规则**

- 派生类的对象可以隐含转换为基类的对象
- 派生类的对象可以初始化基类的引用
- 派生类的指针可以隐含转换为基类的指针，而派生类指针要想转换为基数指针，则转换一个要显示地进行，如

```
 base *pb = new derived();
  derived *pd = static_cast<derived* >(pd)
```


类型兼容规则例子 
```
class b{}
class d:public b{..}
b b1,*p1;
d d1;
b1 = d1;
b &rb = d1;
p1 = &b1;
```

派生类构造函数执行的一般次序：

- 调用基类构造函数，调用顺序按照他们被继承时声明的顺序(从左到右)
- 对派生类新增的成员对象初始化，调用顺序按照他们在类中声明的顺序


为什么复制构造函数使用类对象的引用作为参数，不可以是指针吗？

- 这是因为类型兼容规则。可以用派生类的对象去初始化基类的引用，因此当函数的形参是基类的引用时，实参可以是派生类的对象


当某类的部分或全部直接基类是从另一个共同基类派生而来时，在这些直接基类是从上一级共同基类继承的成员就拥有相同的名称，在派生类的对象中，这些同名数据成员在内存中同时拥有多个副本，同一个函数名会有多个映射。可以使用作用域分辨符来唯一标识访问他们，也可以将共同基类设置为虚基类


在重写继承来的虚函数时，如果函数有默认形参值，不要重新定义不同的值，因为默认的形参值是静态绑定的。另外只有通过基类的指针或者引用调用虚函数时，才会发生动态绑定



如果派生类没有给出纯虚函数的实现，这里派生类仍然是一个抽象类
抽象类不能实例化不能定义对象，但是可以定义一个抽象类的指针或者引用，通过指针或者引用就可以指向并访问派生类的对象，进而访问派生类的成员


**栈和堆的区别**：

栈：栈存在于RAM中。栈是动态的，它的存储速度是第二快的。stack
堆：堆位于RAM中，是一个通用的内存池。所有的对象都存储在堆中。heap

**2 申请方式**

stack【栈】: 由系统自动分配。 例如，声明在函数中一个局部变量 int b; 系统自动在栈中为b开辟空间 。
heap【堆】: 需要程序员自己申请，并指明大小，在c中malloc函数 如p1 = (char *)malloc(10); 在C++中用new运算符 如p2 = (char *)malloc(10); 但是注意：p1、p2本身是在栈中的。

**3 申请后系统的响应**

栈【stack】：只要栈的剩余空间大于所申请空间，系统将为程序提供内存，否则将报异常提示栈溢出。
堆【heap】：首先应该知道操作系统有一个记录空闲内存地址的链表，当系统收到程序的申请时，会遍历该链表，寻找第一个空间大于所申请空间的堆结点，然后将该结点从空闲结点链表中删除，并将该结点的空间分配给程序；另外，对于大多数系统，会在这块内存空间中的首地址处记录本次分配的大小，这样，代码中的delete语句才能正确的释放本内存空间。另外，由于找到的堆结点的大小不一定正好等于申请的大小，系统会自动的将多余的那部分重新放入空闲链表中。

**4 申请大小的限制**

栈【stack】：在Windows下，栈是向低地址扩展的数据结构，是一块连续的内存的区域。这句话的意思是栈顶的地址和栈的最大容量是系统预先规定好的，在WINDOWS下，栈的大小是2M（也有的说是1M，总之是一个编译时就确定的常数），如果申请的空间超过栈的剩余空间时，将提示overflow。因此，能从栈获得的空间较小。




void类型没有分配内存，而引用必须是另一个固定内存变量的别名，所以不能指向void
堆【heap】：堆是向高地址扩展的数据结构，是不连续的内存区域。这是由于系统是用链表来存储的空闲内存地址的，自然是不连续的，而链表的遍历方向是由低地址向高地址。堆的大小受限于计算机系统中有效的虚拟内存。由此可见，堆获得的空间比较灵活，也比较大。

**5 申请效率的比较**

栈【stack】：由系统自动分配，速度较快。但程序员是无法控制的。
堆【heap】：是由new分配的内存，一般速度比较慢，而且容易产生内存碎片，不过用起来最方便.  另外，在WINDOWS下，最好的方式是用VirtualAlloc分配内存，他不是在堆，也不是在栈是直接在进程的地址空间中保留一快内存，虽然用起来最不方便。但是速度快，也最灵活。

**6 堆和栈中的存储内容**

栈【stack】：在函数调用时，第一个进栈的是主函数中后的下一条指令（函数调用语句的下一条可执行语句）的地址，然后是函数的各个参数，在大多数的C编译器中，参数是由右往左入栈的，然后是函数中的局部变量。注意静态变量是不入栈的。  当本次函数调用结束后，局部变量先出栈，然后是参数，最后栈顶指针指向最开始存的地址，也就是主函数中的下一条指令，程序由该点继续运行。
堆【heap】：一般是在堆的头部用一个字节存放堆的大小。堆中的具体内容有程序员安排。 


**7 存取效率的比较** 

`char s1[] = "aaaaaaaaaaaaaaa";  char *s2 = "bbbbbbbbbbbbbbbbb"; ` 

aaaaaaaaaaa是在运行时刻赋值的； 而bbbbbbbbbbb是在编译时就确定的； 但是，在以后的存取中，在栈上的数组比指针所指向的字符串(例如堆)快。





**编译器自动对齐**的原因：<br/>
为了提高程序的性能，数据结构（尤其是栈）应该尽可能地在自然边界上对齐。原因在于，为了访问未对齐的内存，处理器需要作两次内存访问；然而，对齐的内存访问仅需要一次访问。


中断引起的中断处理不是直接由main()引起的，而是由外部事件引起的。


**常数0和空指针**

根据语言定义, 在指针上下文中的常数0 会在编译时转换为空指针。也就是说, 在初始化、赋值或比较的时候,<br/>
如果一边是指针类型的值或表达式, 编译器可以确定另一边的常数0 为空指针并生成正确的空指针值。因此下边的代码段完全合法：<br/>
    char *p = 0;
    if(p != 0)
然而, 传入函数的参数不一定被当作指针环境, 因而编译器可能不能识别未加修饰的0 “表示” 指针。
在函数调用的上下文中生成空指针需要明确的类型转换,强制把0 看作指针。<br/>
例如, Unix 系统调用execl 接受变长的以空指针结束的字符指针参数。它应该如下正确调用：<br/>
execl("/bin/sh", "sh", "-c", "date", (char *)0);<br/>
如果省略最后一个参数的(char *) 转换, 则编译器无从知道这是一个空指针,从而当作一个0 传入。(注意很多Unix 手册在这个例子上都弄错了。)<br/>


**vector**
vector的工作原理是系统预先分配一块CAPACITY大小的空间，当插入的数据超过这个空间的时候，这块空间会让某种方式扩展，但是你删除数据的时候，它却不会缩小。<br/>
vector为了防止大量分配连续内存的开销，保持一块默认的尺寸的内存，clear只是清数据了，未清内存，因为vector的capacity容量未变化，系统维护一个的默认值。<br/>
有什么方法可以释放掉vector中占用的全部内存呢?
标准的解决方法如下

	```
	template < class T >
	void ClearVector( vector< T >& vt )
	{
	vector< T > vtTemp;
	veTemp.swap( vt );
	}
	```

事实上，vector根本就不管内存，它只是负责向内存管理框架acquire/release内存，内存管理框架如果发现内存不够了，就malloc，但是当vector释放资源的时候(比如destruct), stl根本就不调用free以减少内存，因为内存分配在stl的底层：stl假定如果你需要更多的资源就代表你以后也可能需要这么多资源(你的list, hashmap也是用这些内存)，所以就没必要不停地malloc/free。如果是这个逻辑的话这可能是个trade-off<br/>
一般的STL内存管理器allocator都是用内存池来管理内存的，所以某个容器申请内存或释放内存都只是影响到内存池的剩余内存量，而不是真的把内存归还给系统。<br/>
这样做一是为了避免内存碎片，二是提高了内存申请和释放的效率——不用每次都在系统内存里寻找一番。<br/>



vector的数据安排以及操作方式，与array非常相似。两者的唯一区别在于空间的运用的灵活性。array是静态空间，一旦配置了就不能改变；要换个大（或小）一点的房子，可以，一切琐细都得由客户端自己来：首先配置一块新空间，然后将元素从旧址一一搬往新址，再把原来的空间释还给系统。vector是动态空间，随着元素的加入，它的内部机制会自行扩充空间以容纳新元素。 <br/>
因此，vector的运用对于内存的合理利用与运用的灵活性有很大的帮助，我们再也不必因为害怕空间不足而一开始要求一个大块头的array了，我们可以安心使用array，吃多少用多少。 <br/>
vector的实现技术，关键在于其对大小的控制以及重新配置时的数据移动效率。一旦vector的旧有空间满载，如果客户端每新增一个元素，vector的内部只是扩充一个元素的空间，实为不智。因为所谓扩充空间（不论多大），一如稍早所说，是”  配置新空间/数据移动/释还旧空间  “的大工程，时间成本很高，应该加入某种未雨绸缪的考虑。稍后我们便可看到SGI vector的空间配置策略了。 <br/>
另外，由于  vector维护的是一个连续线性空间，所以vector支持随机存取  。 <br/>
注意：vector动态增加大小时，并不是在原空间之后持续新空间（因为无法保证原空间之后尚有可供配置的空间），而是以原大小的两倍另外配置一块较大的空间，然后将原内容拷贝过来，然后才开始在原内容之后构造新元素，并释放原空间。<br/>
因此，  对vector的任何操作，一旦引起空间重新配置，指向原vector的所有迭代器就都失效了  。这是程序员易犯的一个错误，务需小心。<br/>
      

**智能指针**

智能指针是一种资源管理类，通过对原始指针进行封装，在资源管理对象进行析构时对指针指向的内存进行释放；通常使用引用计数方式进行管理，一个基本实现如下：


	```
	class Object;
	class SmartPointer;
	 
	class Counter
	{
	 friend class SmartPointer;
	public:
	 Counter()
	 {
	  ptr = NULL;
	  cnt = 0;
	 }
	 Counter(Object* p)
	 {
	  ptr = p;
	  cnt = 1;
	 }
	 ~Counter()
	 {
	  delete ptr;
	 }
	private:
	 Object* ptr;
	 int cnt;
	};
	 
	class SmartPointer
	{
	public:
	 SmartPointer(Object* p)
	 {
	  ptr_counter = new Counter(p);
	 }
	 SmartPointer(const SmartPointer &sp)
	 {
	  ptr_counter = sp.ptr_counter;
	  ++ptr_count->cnt;
	 }
	 SmartPointer& operator=(const SmartPointer &sp)
	 {
	  ++sp.ptr_counter->cnt;
	  --ptr_counter->cnt;
	  if (ptr_counter->cnt == 0)
	  {
	   delete ptr_counter;
	  }
	  ptr_counter = sp.ptr_counter;
	 }
	 ~SmartPointer()
	 {
	  - -ptr_counter->cnt;
	  if (ptr_counter->cnt == 0)
	  {
	   delete ptr_counter;
	  }
	 }
	private:
	 Counter* ptr_counter;
	 
	};
```

**其他：**

虽然使用数组名时，其会自动转换为指向数组第0个元素，但是需要注意的是数组的首地址是常量。

当数组作为函数实参传递时，传递给函数的是首元素的地址，而将数组某一个元素的地址当作实参时，传递的是此参数的地址，这时可以理解为传递的是子数组(以此元素作为首地址的子数组)的首元素的地址

int a[4][5];

- &a的类型为int(*a)[4][5]
- a+i的类型为Int(*)[5]
- *(a+i)或者a[i]的类型为int *,指向数组a[i]首元素a[i][0]的指针
- &a+i类型为int(*)[5],&a+1使得指针跳过整个数组的大小
- *(*(a+i)+j)的类型为int
- *(a+i)=a[i]
- *(*(a+i)+j)=a[i][j]



共用体占用内存为各成员中占用最大者内存，而结构体占用内存可能超过各成员内存量总和。共用体union和结构体的存放顺序是所有成员都从低地址开始存放

枚举中第一个符号常量对应0，后面的对应前面一个数的下一个整数


sizeof操作符以字节形式给出了其操作数的存储大小，sizeof的计算发生在编译时刻，所以它可以被当作常量表达式使用，会且会无视其括号内的各种运算，如sizeof(a++)中的++不执行

在c等面向过程语言中，局部变量可以和全局变量重名，但是局部变量会屏蔽全局蛮早,重名时，会用到同名的局部变量;若要使用被屏蔽的全局变量需要使用"::"或者extern重新使用全局变量

static的第二个作用是默认初始化为0，包括没有初始化的全局静态变量和局部静态变量。初始化的全局静态变量和局部静态变量就存储在存储在同一块区域内的(BBS段也称为未初始化数据段)

非静态成员在类对象中的排列顺序一致，任何在其中间声明的静态成员都不会被放在对象布局中

static成员函数不能被声明为const，毕竟，将成员函数声明为const就是承诺不会修改该函数所属的对象，而static成员函数不属于任何对象



c中的const意思为一个不能被改变的普通变量，在c中，它总是占用存储，c编译器不能把const视为一个编译期间的常量，在c中，写
    const bufsize = 100;
    int buf[bufsize];
是错误的，这是因为bufsize占用存储的某个地方所以c编译器不知道他编译的值

在c中const int size;是正确的
c编译器把它作为一个声明，这个声明指明在别的地方有存储分配，因为c默认const是外部连接的而c++默认const是内部连接的


- const常量有数据类型而宏常量没有数据类型
- 使用常量可能比使用#define导致更小的目标代码这是因为预处理器盲目地将宏名称替换为其代替的值
- 同时const还可以执行常量折叠，也就是说编译器在编译时可以通过必要的计算把一个复杂的常量表达式缩减成简单的

函数可返回的指针是指向堆中分配的存储空间的指针或指向静态存储区的指针，在函数返回后它仍然有效


如果两个成员函数只是常量性不同，可以被重载，如
    class base {
      void func();
      void func() const;
    };

const成员变量不能在类定义处初始化，只能通过构造函数初始化列表进行，并且必须有构造函数，const数据成员只在某个对象生存期内是常量而对于整个类而言却是可变的，因为类可以创建多个对象，不同的对象其const数据成员的值可以不同，所以不能在类的声明中初始化const数据成员，因为类的对象还没有被创建时，编译器不乱放const数据成员的值是什么

给const static成员初始化时，不需要加static修饰符，但要加const

new内置了sizeof、类型转换和类型安全检查功能<br/>
对于非内部数据类型的对象而言，new在创建动态对象的同时完成了初始化工作;如果用new创建对象数组时，那么只能使用对象的无参数构造函数

    object *objects = new object[100](1);//是错误的



内存池是一种分配方式，真正使用内存之前，先申请分配一定数量的大小相等的内存块留作备用。尽量避免了内存碎片

const只能作用于成员函数不能作用于全局函数

int *&v的定义从右到左理解，v1是一个引用，与指向int型对象的指针相关联。也就是说v1只是传递进函数的任意指针的别名


**extern "c"的作用**

c++语言是一种面向对象编程的语言，为了支持重载机制，在编译生成的汇编码中，要对函数的名字进行一些处理，加入比如函数返回类型等信息，而在c语言中，只是简单的函数名字而已，不会加入其他的信息，也就是说:c++和c语言对产生的函数名字的处理不一样的，这样在链接阶段若是按照c++的函数命名规则去查找c编译器编译的函数就会出现链接错误

*p++与(*P)++不等价，*优先级比++高，*p++先取值操作，然后对指针地址执行++，（*p)++先取值操作，然后对值执行++


    typedef string *pstring
    const pstring cstr
    等价于string *const cstr

指向重载函数的指针，指针类型必须与重载函数的一个版本精确匹配，参数和返回值匹配


如果返回动态分配的对象或者内存，必须使用指针，引用可能引起内存溢出

引用本质只是一个对象的别名，对引用别名的操作就是对本身变量的操作，而不是修改引用使其绑定到其他变量上

    char *c[] = {"ENTER","NEW","POINT","TIRST"};
    char **cp = {c+3,c+2,c+1,c};
    char ***cpp = cp;
    int main(void) {
      	printf("%s",**++cpp);//POINT
    	printf("%s",*--*++cpp+3);//ER
    	printf("%s",*cpp[-2]+3);//ST
    	printf("%s",cpp[-1][-1]+1);//EW
    	return 0;
    }


内置或复合类型的成员的初始化值依赖于对象的作用域，在局部作用域中这些成员不被初始化，而在全局作用域中它们被初始化为0
比如

    class student {
      public:
    	student(){};
    	void show();
     private:
       string name;
       int number;
    	int score;
    };
    student a;
    int main() {
      student b;
    }
a/b的各个成员变量值是多少


浅复制：被复制的对象的所有变量都含有与原来的对象相同的值，而所有的对其他对象的引用仍然指向原来的对象

若是处于安全状态，某一进程再提出申请，很有可能从安全状态变为不安全状态，也有可能发生死锁。系统处于不安全状态很可能发生死锁，若存在死锁，一定存在不安全状态

c++中空类默认产生那些成员函数？

    class empty {
      public:
     empty();
    	empty(const empty&);//复制构造
    	~empty();
    	empty& operator=(const empty&);
    	empty* operator&();//取址运算符
    	const empty* operator&() const;//取址运算符const
    };

在公有继承方式，派生类的对象/对象指针/对象引用可以赋值给基类的对象/对象指针/对象引用（发生隐式转换），反之不能，因为基类缺乏派生类中的信息


- 使用指针访问非虚函数时，编译器根据指针本身的类型决定要调用哪个函数，而不是根据指针指向的对象类型
- 使用指针访问虚函数时，编译器根据指向的对象类型决定要调用哪个函数，而不是根据指针本身的类型


普通函数(非成员函数)只能被重载不能被覆盖，声明为虚函数也没有任何意义，因此编译器会在编译时绑定函数

构造函数和析构函数是特殊的成员函数，在其中访问虚函数时，c++采用静态联编，也就是说在构造函数或析构函数内，即使是使用this->虚函数名的形式调用，编译器仍然将其解释为静态联编的"本类名::虚函数名"，因而这样会与使用者的意图不符

凡是含有纯虚函数的类称为抽象类，这种类不能声明对象，只是作为基类为派生服务，除非在派生类中完全实现基类中所有的纯虚函数，否则，派生类也是抽象类，不能实例化对象


抽象类不能定义对象，但是可以作为指针或者引用类型使用


抽象类中的纯虚函数没有具体的实现，所以不能实例化