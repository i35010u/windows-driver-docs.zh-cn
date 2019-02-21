---
title: 使用 UMDH 来查找用户模式内存泄漏
description: 使用 UMDH 来查找用户模式内存泄漏
ms.assetid: b15ed695-3f35-4a72-93ab-3cbfd2e33980
keywords:
- 内存泄漏，用户模式下，UMDH
- UMDH，内存泄漏检测
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f215d8e02eeee80cc4a38a80b61a423c9c86d7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524740"
---
# <a name="using-umdh-to-find-a-user-mode-memory-leak"></a>使用 UMDH 来查找用户模式内存泄漏


用户模式转储堆 (UMDH) 实用工具适用于要分析特定进程的 Windows 堆分配的操作系统。 UMDH 查找特定的进程中的例程正在泄漏内存。

UMDH 包含在为 Windows 调试工具。 有关完整详细信息，请参阅[UMDH](umdh.md)。

### <a name="span-idpreparingtouseumdhspanspan-idpreparingtouseumdhspanpreparing-to-use-umdh"></a><span id="preparing_to_use_umdh"></span><span id="PREPARING_TO_USE_UMDH"></span>准备使用 UMDH

如果你不已确定哪个进程正在泄漏内存，请先输入。 有关详细信息，请参阅[查找用户模式内存泄漏到使用性能监视器](using-performance-monitor-to-find-a-user-mode-memory-leak.md)。

UMDH 日志中最重要的数据是堆分配的堆栈跟踪。 若要确定进程是否正在泄漏堆内存，分析这些堆栈跟踪。

在使用之前 UMDH 以显示堆栈跟踪数据，必须使用[GFlags](gflags.md)正确配置您的系统。 GFlags 包含在为 Windows 调试工具。

以下 GFlags 设置启用 UMDH 堆栈跟踪：

-   在 GFlags 图形界面中，选择映像文件选项卡，键入进程名称 （包括文件扩展名），按 TAB 键，选择**创建用户模式堆栈跟踪数据库**，然后单击**应用**.

    或者，也可以说，使用以下 GFlags 命令行，其中*ImageName*进程名称 （包括文件扩展名）：

    ```dbgcmd
    gflags /i ImageName +ust 
    ```
    使用此命令完成后清除 GFlag 设置。 有关详细信息，请参阅[GFlags 命令](gflags-commands.md)。

    ```dbgcmd
    gflags /i ImageName -ust 
    ```
    

-   默认情况下，Windows 将收集的堆栈跟踪数据量是限制为 32 MB x86 处理器和 64 MB 在 x64 处理器。 如果必须增加此数据库的大小，请选择**映像文件**GFlags 图形界面中的选项卡上，键入进程名称，按 TAB 键，检查**堆栈回溯 （兆字节）** 复选框，键入在相关的文本框中，值 （以 mb 为单位），然后单击**应用**。 增加时有必要，则只有此数据库，因为它可能会耗尽有限的 Windows 资源。 当不再需要较大的大小时，则将此设置恢复到其原始值。

-   如果在更改任何标志**系统注册表**选项卡上，您必须重新启动 Windows 以使这些更改生效。 如果在更改任何标志**映像文件**选项卡上，你必须重新启动进程，以使更改生效。 将更改为**内核标志**选项卡将立即生效，但它们都将丢失下次重启 Windows。

在使用之前 UMDH，必须为应用程序具有访问正确的符号。 UMDH 使用环境变量指定的符号路径\_NT\_符号\_路径。 设置为包含你的应用程序的符号的路径，此变量等。 如果还包括 Windows 符号的路径，分析可能会更完整。 此符号路径的语法等同于使用的调试器;有关详细信息，请参阅[符号路径](symbol-path.md)。

例如，如果你的应用程序的符号位于 c:\\MySymbols，并且您想要使用公共 Microsoft 符号存储区的 Windows 符号，使用 c:\\MyCache 将作为下游存储，使用以下命令若要设置符号路径：

```console
set _NT_SYMBOL_PATH=c:\mysymbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols 
```

此外，若要确保准确的结果，您必须禁用 BSTR 缓存。 若要执行此操作，请将 OANOCACHE 环境变量设置为一 (1)。 进行此设置，然后启动其分配是要跟踪的应用程序。

如果需要跟踪由服务进行的分配，你必须将 OANOCACHE 设置为系统环境变量，然后重新为此设置的 Windows 才会生效。


### <a name="span-iddetectingincreasesinheapallocationswithumdhspanspan-iddetectingincreasesinheapallocationswithumdhspandetecting-increases-in-heap-allocations-with-umdh"></a><span id="detecting_increases_in_heap_allocations_with_umdh"></span><span id="DETECTING_INCREASES_IN_HEAP_ALLOCATIONS_WITH_UMDH"></span>检测堆分配，则使用 UMDH 增加

这些准备后，可以使用 UMDH 来捕获有关进程的堆分配信息。 若要执行此操作，请使用以下过程：

1.  确定[进程 ID (PID)](finding-the-process-id.md)为想要调查的过程。

2.  使用 UMDH 分析的堆内存分配的这一过程，并将其保存到日志文件。 -P 开关 PID，并使用日志文件的名称-f 开关一起使用。 例如，如果 PID 为 124，并且你想要将日志文件 Log1.txt，使用以下命令：

    ```console
    umdh -p:124 -f:log1.txt 
    ```dbgcmd

3.  Use Notepad or another program to open the log file. This file contains the call stack for each heap allocation, the number of allocations made through that call stack, and the number of bytes consumed through that call stack.

4.  Because you are looking for a memory leak, the contents of a single log file are not sufficient. You must compare log files recorded at different times to determine which allocations are growing.

    UMDH can compare two different log files and display the change in their respective allocation sizes. You can use the greater-than symbol (**&gt;**) to redirect the results into a third text file. You may also want to include the -d option, which converts the byte and allocation counts from hexadecimal to decimal. For example, to compare Log1.txt and Log2.txt, saving the results of the comparison to the file LogCompare.txt, use the following command:

    ```console
    umdh log1.txt log2.txt > logcompare.txt 
    ```

5.  打开 LogCompare.txt 文件。 其内容如下所示：

    ```text
    + 5320 ( f110 - 9df0) 3a allocs BackTrace00B53 
    Total increase == 5320 
    ```

    对于每个调用堆栈 （标记为"回溯"） UMDH 日志文件中，没有两个日志文件之间进行比较。 在此示例中，第一个日志的文件 (Log1.txt) 捕获分配给 BackTrace00B53，而第二个日志文件记录 0xF110 字节，这意味着，没有 0x5320 其他分配的字节数的这段时间的两个日志记录的 0x9DF0 字节。 调用堆栈由 BackTrace00B53 标识来自字节。

6.  若要确定该反向跟踪中，打开其中一个原始日志文件 (例如，Log2.txt) 并搜索"BackTrace00B53。" 其结果是类似于此数据：

    ```text
    00005320 bytes in 0x14 allocations (@ 0x00000428) by: BackTrace00B53
    ntdll!RtlDebugAllocateHeap+0x000000FD
    ntdll!RtlAllocateHeapSlowly+0x0000005A
    ntdll!RtlAllocateHeap+0x00000808
    MyApp!_heap_alloc_base+0x00000069
    MyApp!_heap_alloc_dbg+0x000001A2
    MyApp!_nh_malloc_dbg+0x00000023
    MyApp!_nh_malloc+0x00000016
    MyApp!operator new+0x0000000E
    MyApp!DisplayMyGraphics+0x0000001E
    MyApp!main+0x0000002C
    MyApp!mainCRTStartup+0x000000FC
    KERNEL32!BaseProcessStart+0x0000003D 
    ```

    此 UMDH 输出显示了 0x5320 (十进制 21280) 从调用堆栈中分配的总字节数。 这些已分配的字节数从 0x14 (十进制 20) 单独分配的 0x428 (十进制 1064) 个字节。

    调用堆栈在给出的"BackTrace00B53"，并显示此堆栈中的调用。 在查看调用堆栈，可以看到**DisplayMyGraphics**例程分配通过内存**新**运算符，调用例程*malloc*，使用要获取从堆内存的 Visual c + + 运行时库。

    确定这些调用哪一项要显式显示在源代码中的最后一个。 在这种情况下，最好**新**运算符因为调用*malloc*实现的过程中发生**新**而不是单独分配。 因此的此实例**新**中的运算符**DisplayMyGraphics**例程反复分配不释放的内存。

 

 





