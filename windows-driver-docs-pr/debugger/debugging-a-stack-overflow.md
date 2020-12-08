---
title: 调试堆栈溢出
description: 调试堆栈溢出
keywords:
- 堆栈溢出
- 调用堆栈，调试堆栈溢出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16086c95b0595bf4725705d61b65f99f4c7bbd6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803631"
---
# <a name="debugging-a-stack-overflow"></a>调试堆栈溢出


## <span id="ddk_debugging_a_stack_overflow_dbg"></span><span id="DDK_DEBUGGING_A_STACK_OVERFLOW_DBG"></span>


堆栈溢出是用户模式线程可能会遇到的错误。 导致此错误的可能原因有三个：

-   线程使用为其保留的整个堆栈。 这通常是由于无限递归导致的。

-   线程无法扩展堆栈，因为页文件已极限，因此不能提交其他页来扩展堆栈。

-   线程无法扩展堆栈，因为系统在用于扩展页面文件的短时间内。

当线程上运行的函数分配本地变量时，变量将放在线程的调用堆栈上。 函数所需的堆栈空间量可能与所有局部变量的大小之和相同。 但编译器通常会执行优化，以减少函数所需的堆栈空间。 例如，如果两个变量在不同的范围内，则编译器可以对这两个变量使用相同的堆栈内存。 编译器还可以通过优化计算来完全消除某些局部变量。

优化量受生成时应用的编译器设置的影响。 例如，调试版本和发布版本具有不同的优化级别。 调试版本中的函数所需的堆栈空间量可能大于发布版本中该相同函数所需的堆栈空间量。

下面是如何调试堆栈溢出的示例。 在此示例中，NTSD 与目标应用程序运行在同一台计算机上，并将其输出重定向到主计算机上的 KD。 有关详细信息，请参阅 [控制内核调试器中的 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) 。

第一步是确定导致调试器中断的事件：

```dbgcmd
0:002> .lastevent 
Last event: Exception C00000FD, second chance 
```

可以在 ntstatus 中查找异常代码0xC00000FD，该代码可在 Microsoft Windows SDK 和 Windows 驱动程序工具包 (WDK) 中找到。 此异常代码为状态 \_ 堆栈 \_ 溢出。

若要仔细检查堆栈是否溢出，可以使用 [**k (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令：

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

目标线程已中断到 COMCTL32.DLL！ \_chkstk，指示堆栈问题。 现在应调查目标进程的堆栈使用情况。 该进程具有多个线程，但重要的是导致溢出的线程，因此首先识别此线程：

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

现在需要调查线程2。 此行左侧的时间段指示这是当前线程。

堆栈信息包含在0x7FFDC000 上的 TEB (线程环境块) 中。 列出它的最简单方法是使用 [**！ teb**](-teb.md)。 但是，这要求您具有适当的符号。 为实现最大通用性，假设你没有符号：

```dbgcmd
0:002> dd 7ffdc000 L4 
7ffdc000   009fdef0 00a00000 009fc000 00000000 
```

若要解释这一点，您需要查找 TEB 数据结构的定义。 如果有完整的符号，可以使用 [**DT TEB**](dt--display-type-.md) 来执行此操作。 但在这种情况下，你将需要查看 Microsoft Windows SDK 中的 ntpsapi 文件。 此文件包含以下信息：

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

这表示 TEB 结构中的第二个和第三个 Dword 分别指向堆栈的底部和顶部。 在这种情况下，这些地址是0x00A00000 和0x009FC000。  (堆栈在内存中向下扩展。 ) 可以使用 [**？ (计算表达式)**](---evaluate-expression-.md) 命令来计算堆栈大小：

```dbgcmd
0:002> ? a00000-9fc000
Evaluate expression: 16384 = 00004000 
```

这表明堆栈大小为 16 K。最大堆栈大小存储在字段 **DeallocationStack** 中。 在进行某些计算后，可以确定此字段的偏移量是否为0xE0C。

```dbgcmd
0:002> dd 7ffdc000+e0c L1 
7ffdce0c   009c0000 

0:002> ? a00000-9c0000 
Evaluate expression: 262144 = 00040000 
```

这表明最大堆栈大小为 256 K，这表示剩余的堆栈空间已足够。

此外，此过程看起来很简单--它不在无限递归中，或通过使用过大的基于堆栈的数据结构而超出其堆栈空间。

现在，中断 KD，并使用 [**！ vm**](-vm.md) extension 命令查看总体系统内存使用情况：

```dbgcmd
0:002> .breakin 
Break instruction exception - code 80000003 (first chance)
ntoskrnl!_DbgBreakPointWithStatus+4:
80148f9c cc               int     3

kd> !vm 

**_ Virtual Memory Usage _*_
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

首先，查看未分页的池使用情况。 两者都在限制范围内，因此不是问题的原因。

接下来，查看提交的页数： 183528/202280。 这非常接近于限制。 尽管此显示不会将此数量完全显示为限制，但你应记住，在执行用户模式调试时，其他进程正在系统上运行。 每次执行 NTSD 命令时，这些其他进程也会分配和释放内存。 这意味着，当发生堆栈溢出时，您不会确切地了解内存状态。 如果已提交的页码接近于限制值，则有合理的结论是在某个时间点使用了页面文件，这导致了堆栈溢出。

这并不是一种常见情况，因此，目标应用程序不能真正出错。 如果经常发生这种情况，则可能需要考虑为发生故障的应用程序引发初始堆栈承诺。

### <a name="span-idanalyzing_a_single_function_callspanspan-idanalyzing_a_single_function_callspananalyzing-a-single-function-call"></a><span id="analyzing_a_single_function_call"></span><span id="ANALYZING_A_SINGLE_FUNCTION_CALL"></span>分析单个函数调用

它还有助于准确了解某个函数调用分配的堆栈空间量。

要执行此操作，请先拆装前面几个说明，然后查找 `sub esp` _number * 的指令。 这会移动堆栈指针，有效地保留本地数据的 *数字* 字节。

以下是示例：

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

这会显示 **标头 \_ 绘图** 为堆栈空间分配的0x58 字节数。

 

 





