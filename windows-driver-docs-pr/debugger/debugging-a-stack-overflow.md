---
title: 调试堆栈溢出
description: 调试堆栈溢出
ms.assetid: fc67effa-88c9-4915-a5a8-8c094595c6c5
keywords:
- 堆栈溢出
- 调用堆栈，调试堆栈溢出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96477c41a79a1695d5123e404ceea89eebd92d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541046"
---
# <a name="debugging-a-stack-overflow"></a>调试堆栈溢出


## <span id="ddk_debugging_a_stack_overflow_dbg"></span><span id="DDK_DEBUGGING_A_STACK_OVERFLOW_DBG"></span>


Stack overflow 是用户模式线程可能会遇到的错误。 有三个可能的原因，此错误：

-   一个线程使用为其保留在整个堆栈。 这通常被引起的无限递归。

-   一个线程不能扩展堆栈，因为页面文件就会大大提高，并因此没有其他页就可提交扩展堆栈。

-   由于系统内使用，以扩展页面文件的短时间内，线程不能扩展堆栈。

当一个线程上运行的函数分配的本地变量时，变量放线程的调用堆栈上。 函数所需的堆栈空间量可能大至所有本地变量的大小的总和。 但是，编译器通常会执行优化，降低函数所需的堆栈空间。 例如，如果两个变量，则在不同的作用域中，编译器可以为这两个这些变量使用相同的堆栈内存。 编译器还可能无法完全消除某些本地变量对计算进行优化。

优化的量会影响应用在生成时的编译器设置。 例如，调试版本和发布版本具有不同的优化级别。 所需的调试版本中的函数的堆栈空间量可能会大于该发行版中的相同函数所需的堆栈空间量。

下面是举例说明如何调试堆栈溢出。 在此示例中，NTSD 作为目标应用程序在同一计算机上运行，并为其将输出重定向到 KD 主机计算机上。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

第一步是确认哪些事件导致调试器中断：

```dbgcmd
0:002> .lastevent 
Last event: Exception C00000FD, second chance 
```

您可以查找异常代码 0xC00000FD ntstatus.h，可在 Microsoft Windows SDK 和 Windows Driver Kit (WDK) 中。 此异常代码是状态\_堆栈\_溢出。

若要仔细检查堆栈溢出，可以使用[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令：

```dbgcmd
0:002> k 
ChildEBP RetAddr
009fdd0c 71a32520 COMCTL32!_chkstk+0x25
009fde78 77cf8290 COMCTL32!ListView_WndProc+0x4c4
009fde98 77cfd634 USER32!_InternalCallWinProc+0x18
009fdf00 77cd55e9 USER32!UserCallWinProcCheckWow+0x17f
009fdf3c 77cd63b2 USER32!SendMessageWorker+0x4a3
009fdf5c 71a45b30 USER32!SendMessageW+0x44
009fdfec 71a45bb0 COMCTL32!CCSendNotify+0xc0e
009fdffc 71a1d688 COMCTL32!CICustomDrawNotify+0x2a
009fe074 71a1db30 COMCTL32!Header_Draw+0x63
009fe0d0 71a1f196 COMCTL32!Header_OnPaint+0x3f
009fe128 77cf8290 COMCTL32!Header_WndProc+0x4e2
009fe148 77cfd634 USER32!_InternalCallWinProc+0x18
009fe1b0 77cd4490 USER32!UserCallWinProcCheckWow+0x17f
009fe1d8 77cd46c8 USER32!DispatchClientMessage+0x31
009fe200 77f7bb3f USER32!__fnDWORD+0x22
009fe220 77cd445e ntdll!_KiUserCallbackDispatcher+0x13
009fe27c 77cfd634 USER32!DispatchMessageWorker+0x3bc
009fe2e4 009fe4a8 USER32!UserCallWinProcCheckWow+0x17f
00000000 00000000 0x9fe4a8 
```

目标线程已分解成 COMCTL32 ！\_chkstk，指示堆栈问题。 现在您应该调查目标进程的堆栈使用情况。 进程具有多个线程，但重要的一项是指导致溢出，因此首先标识此线程：

```dbgcmd
0:002> ~*k

   0  id: 570.574   Suspend: 1 Teb 7ffde000 Unfrozen
   .....

   1  id: 570.590   Suspend: 1 Teb 7ffdd000 Unfrozen
   .....

. 2  id: 570.598   Suspend: 1 Teb 7ffdc000 Unfrozen
ChildEBP RetAddr
 009fdd0c 71a32520 COMCTL32!_chkstk+0x25 
.....

   3  id: 570.760   Suspend: 1 Teb 7ffdb000 Unfrozen 
```

现在，您需要调查线程 2。 在这行左侧句点指示这是当前线程。

在 0x7FFDC000 TEB （线程环境块） 中包含的堆栈信息。 若要将其列的最简单方法使用[ **！ teb**](-teb.md)。 但是，这需要您具有正确的符号。 最大用途广泛，假定您有没有符号：

```dbgcmd
0:002> dd 7ffdc000 L4 
7ffdc000   009fdef0 00a00000 009fc000 00000000 
```

若要对此进行解释，需要查找 TEB 数据结构的定义。 如果具有完整符号，则可以使用[ **dt TEB** ](dt--display-type-.md)若要执行此操作。 但在这种情况下，你将需要看一下 Microsoft Windows SDK 中的 ntpsapi.h 文件。 此文件包含以下信息：

```cpp
typedef struct _TEB {
    NT_TIB NtTib;
    PVOID  EnvironmentPointer;
    CLIENT_ID ClientId;
    PVOID ActiveRpcHandle;
    PVOID ThreadLocalStoragePointer;
    PPEB ProcessEnvironmentBlock;
    ULONG LastErrorValue;
    .....
    PVOID DeallocationStack;
    .....
} TEB;

typedef struct _NT_TIB {
    struct _EXCEPTION_REGISTRATION_RECORD *ExceptionList;
    PVOID StackBase;
    PVOID StackLimit;
    .....
} NT_TIB; 
```

这表示 TEB 第二个和第三个 dword 值分别结构指向堆栈的顶部和底部。 在这种情况下，这些地址是 0x00A00000 和 0x009FC000。 （堆栈增长向下拖动在内存中。）可以使用堆栈大小来计算[ **？（计算表达式）** ](---evaluate-expression-.md)命令：

```dbgcmd
0:002> ? a00000-9fc000
Evaluate expression: 16384 = 00004000 
```

这将显示的堆栈大小是 16 k。字段中存储的最大堆栈大小**DeallocationStack**。 一些计算之后, 可以确定该字段的偏移量是 0xE0C。

```dbgcmd
0:002> dd 7ffdc000+e0c L1 
7ffdce0c   009c0000 

0:002> ? a00000-9c0000 
Evaluate expression: 262144 = 00040000 
```

这将显示最大堆栈大小为 256k，这意味着多个剩余足够的堆栈空间。

此外，此过程看起来干净--它不是无穷递归或通过使用过大基于堆栈的数据结构来超出它的堆栈空间中。

现在将拆分为 KD 并看看与整体的系统内存使用量[ **！ vm** ](-vm.md)扩展命令：

```dbgcmd
0:002> .breakin 
Break instruction exception - code 80000003 (first chance)
ntoskrnl!_DbgBreakPointWithStatus+4:
80148f9c cc               int     3

kd> !vm 

*** Virtual Memory Usage ***
        Physical Memory:     16268   (   65072 Kb)
        Page File: \??\C:\pagefile.sys
           Current:    147456Kb Free Space:     65988Kb
           Minimum:     98304Kb Maximum:       196608Kb
        Available Pages:      2299   (    9196 Kb)
        ResAvail Pages:       4579   (   18316 Kb)
        Locked IO Pages:        93   (     372 Kb)
        Free System PTEs:    42754   (  171016 Kb)
        Free NP PTEs:         5402   (   21608 Kb)
        Free Special NP:       348   (    1392 Kb)
        Modified Pages:        757   (    3028 Kb)
        NonPagedPool Usage:    811   (    3244 Kb)
        NonPagedPool Max:     6252   (   25008 Kb)
        PagedPool 0 Usage:    1337   (    5348 Kb)
        PagedPool 1 Usage:     893   (    3572 Kb)
        PagedPool 2 Usage:     362   (    1448 Kb)
        PagedPool Usage:      2592   (   10368 Kb)
        PagedPool Maximum:   13312   (   53248 Kb)
        Shared Commit:        3928   (   15712 Kb)
        Special Pool:         1040   (    4160 Kb)
        Shared Process:       3641   (   14564 Kb)
        PagedPool Commit:     2592   (   10368 Kb)
        Driver Commit:         887   (    3548 Kb)
        Committed pages:     45882   (  183528 Kb)
        Commit limit:        50570   (  202280 Kb)

        Total Private:       33309   (  133236 Kb)
         ..... 
```

首先，看一下非分页和页面缓冲池使用情况。 这两个完全符合限制，因此这些不是问题的原因。

接下来，查看的已提交的页数：带 202280 183528。 这是非常接近的限制。 尽管此显示不显示此数量是完全的限制，但您应牢记于心执行用户模式下调试时其他进程在系统上运行。 每次执行 NTSD 命令时，这些其他进程也分配和释放内存。 这意味着您不知道确切的内存状态是什么等发生堆栈溢出时。 鉴于此限制的接近程度已提交的页码是，有理由得出结论： 在某一时刻的页面文件已用完，这导致堆栈溢出。

这不是少见的匹配项，且确实不能为此出现故障的目标应用程序。 如果经常发生，你可能想要应考虑引发故障的应用程序的初始堆栈承诺。

### <a name="span-idanalyzingasinglefunctioncallspanspan-idanalyzingasinglefunctioncallspananalyzing-a-single-function-call"></a><span id="analyzing_a_single_function_call"></span><span id="ANALYZING_A_SINGLE_FUNCTION_CALL"></span>分析单个函数调用

它还可用于找出特定函数调用分配完全堆栈空间量。

若要执行此操作，拆装第一个几条指令，并查找指令`sub esp`*数*。 这将有效地保留的堆栈指针*数*本地数据的字节数。

下面是一个示例：

```dbgcmd
0:002> k 
ChildEBP RetAddr
009fdd0c 71a32520 COMCTL32!_chkstk+0x25
009fde78 77cf8290 COMCTL32!ListView_WndProc+0x4c4
009fde98 77cfd634 USER32!_InternalCallWinProc+0x18
009fdf00 77cd55e9 USER32!UserCallWinProcCheckWow+0x17f
009fdf3c 77cd63b2 USER32!SendMessageWorker+0x4a3
009fdf5c 71a45b30 USER32!SendMessageW+0x44
009fdfec 71a45bb0 COMCTL32!CCSendNotify+0xc0e
009fdffc 71a1d688 COMCTL32!CICustomDrawNotify+0x2a
009fe074 71a1db30 COMCTL32!Header_Draw+0x63
009fe0d0 71a1f196 COMCTL32!Header_OnPaint+0x3f
009fe128 77cf8290 COMCTL32!Header_WndProc+0x4e2

0:002> u COMCTL32!Header_Draw
 COMCTL32!Header_Draw :
71a1d625 55               push    ebp
71a1d626 8bec             mov     ebp,esp
71a1d628 83ec58           sub     esp,0x58
71a1d62b 53               push    ebx
71a1d62c 8b5d08           mov     ebx,[ebp+0x8]
71a1d62f 56               push    esi
71a1d630 57               push    edi
71a1d631 33f6             xor     esi,esi 
```

这表明**标头\_绘制**分配 0x58 字节的堆栈空间。

 

 





