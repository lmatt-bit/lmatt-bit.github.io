Title: #pragma（转载自百度百科)
Date: 2010-03-19 18:42
Author: lmatt wang
Slug: pragmazhuanzaizibaidubaike

[\#pragma](http://baike.baidu.com/view/1451188.htm)
===================================================

\#pragma 预处理指令详解\
在所有的预处理指令中，\#Pragma
指令可能是最复杂的了，它的作用是设定编译器的状态或者是指示编译器完成一些特定的动作。\#pragma指令对每个编译器给出了一个方法,在保持与C和
C++语言完全兼容的情况下,给出主机或操作系统专有的特征。依据定义,编译指示是机器或操作系统专有的,且对于每个编译器都是不同的。\
其格式一般为: \#Pragma Para\
其中Para 为参数，下面来看一些常用的参数。\
(1)message 参数。 Message
参数能够在编译信息输出窗口中输出相应的信息，这对于源代码信息的控制是非常重要的。其使用方法为：\
\#Pragma message(“消息文本”)\
当编译器遇到这条指令时就在编译输出窗口中将消息文本打印出来。\
当我们在程序中定义了许多宏来控制源代码版本的时候，我们自己有可能都会忘记有没有正确的设置这些宏，此时我们可以用这条指令在编译的时候就进行检查。假设我们希望判断自己有没有在源代码的什么地方定义了\_X86这个宏可以用下面的方法\
\#ifdef \_X86\
\#Pragma message(“\_X86 macro activated!”)\
\#endif\
当我们定义了\_X86这个宏以后，应用程序在编译时就会在编译输出窗口里显示“\_X86
macro
activated!”。我们就不会因为不记得自己定义的一些特定的宏而抓耳挠腮了。\
(2)另一个使用得比较多的pragma参数是code\_seg。格式如：\
\#pragma code\_seg( ["section-name"[,"section-class"] ] )\
它能够设置程序中函数代码存放的代码段，当我们开发驱动程序的时候就会使用到它。\
(3)\#pragma once (比较常用）\
只要在头文件的最开始加入这条指令就能够保证头文件被编译一次，这条指令实际上在VC6中就已经有了，但是考虑到兼容性并没有太多的使用它。\
\#pragma
once是编译相关，就是说这个编译系统上能用，但在其他编译系统不一定可以，也就是说移植性差，不过现在基本上已经是每个编译器都有这个定义了。\
(4)\#pragma
hdrstop表示预编译头文件到此为止，后面的头文件不进行预编译。BCB可以预编译头文件以加快链接的速度，但如果所有头文件都进行预编译又可能占太多磁盘空间，所以使用这个选项排除一些头文件。\
有时单元之间有依赖关系，比如单元A依赖单元B，所以单元B要先于单元A编译。你可以用\#pragma
startup指定编译优先级，如果使用了\#pragma package(smart\_init)
，BCB就会根据优先级的大小先后编译。\
(5)\#pragma resource
"\*.dfm"表示把\*.dfm文件中的资源加入工程。\*.dfm中包括窗体外观的定义。\
(6)\#pragma warning( disable : 4507 34; once : 4385; error : 164 )\
等价于：\
\#pragma warning(disable:4507 34) // 不显示4507和34号警告信息\
\#pragma warning(once:4385) // 4385号警告信息仅报告一次\
\#pragma warning(error:164) // 把164号警告信息作为一个错误。\
同时这个pragma warning 也支持如下格式：\
\#pragma warning( push [ ,n ] )\
\#pragma warning( pop )\
这里n代表一个警告等级(1---4)。\
\#pragma warning( push )保存所有警告信息的现有的警告状态。\
\#pragma warning( push,
n)保存所有警告信息的现有的警告状态，并且把全局警告等级设定为n。\
\#pragma warning( pop )向栈中弹出最后一个警告信息，\
在入栈和出栈之间所作的一切改动取消。例如：\
\#pragma warning( push )\
\#pragma warning( disable : 4705 )\
\#pragma warning( disable : 4706 )\
\#pragma warning( disable : 4707 )\
//.......\
\#pragma warning( pop )\
在这段代码的最后，重新保存所有的警告信息(包括4705，4706和4707)。\
(7)pragma comment(...)\
该指令将一个注释记录放入一个对象文件或可执行文件中。\
常用的lib关键字，可以帮我们连入一个[库文件](http://baike.baidu.com/view/1595059.htm)。\
每个编译程序可以用\#pragma指令激活或终止该编译程序支持的一些编译功能。例如，对循环优化功能：\
\#pragma loop\_opt(on) // 激活\
\#pragma loop\_opt(off) // 终止\
有时，程序中会有些函数会使编译器发出你熟知而想忽略的警告，如“Parameter
xxx is never used in function xxx”，可以这样：\
\#pragma warn —100 // Turn off the warning message for warning \#100\
int insert\_record(REC \*r)\
{ /\* function body \*/ }\
\#pragma warn +100 // Turn the warning message for warning \#100 back
on\
函数会产生一条有唯一特征码100的警告信息，如此可暂时终止该警告。\
每个编译器对\#pragma的实现不同，在一个编译器中有效在别的编译器中几乎无效。可从编译器的文档中查看。\
\#pragma pack(n)和\#pragma pack()\
struct sample\
{\
char a;\
double b;\
};\
当sample结构没有加\#pragma pack(n)的时候,sample按最大的成员那个对齐;\
（所谓的对齐是指对齐数为n时,对每个成员进行对齐,既如果成员a的大小小于n则将a扩大到n个大小;\
如果a的大小大于n则使用a的大小;）所以上面那个结构的大小为16字节.\
当sample结构加\#pragma pack(1)的时候,sizeof(sample)=9字节;无空字节。\
（另注：当n大于sample结构的最大成员的大小时，n取最大成员的大小。\
所以当n越大时，结构的速度越快，大小越大；反之则）\
\#pragma pack()就是取消\#pragma
pack(n)的意思了，也就是说接下来的结构不用\#pragma pack(n)\

> 文章中引用到<http://blog.csdn.net/wrq147/archive/2009/07/31/4398674.aspx>
> </p>

补充：pragma comment(lib, "xx.lib"),用于导入某个库
