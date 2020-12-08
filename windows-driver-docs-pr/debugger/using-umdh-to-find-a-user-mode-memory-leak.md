---
title: 使用 UMDH 查找用户模式内存泄漏
description: 使用 UMDH 查找用户模式内存泄漏
keywords:
- 内存泄漏，用户模式，UMDH
- UMDH，内存泄漏检测
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: b7cc0e921dd9df6ccddc3634687593b8a1de376d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803011"
---
# <a name="using-umdh-to-find-a-user-mode-memory-leak"></a>使用 UMDH 查找用户模式内存泄漏


用户模式转储堆 (UMDH) 实用工具与操作系统一起用于分析特定进程的 Windows 堆分配。 UMDH 查找特定进程中的哪个例程正在泄漏内存。

UMDH 包含在 Windows 调试工具中。 有关完整详细信息，请参阅 [UMDH](umdh.md)。

### <a name="span-idpreparing_to_use_umdhspanspan-idpreparing_to_use_umdhspanpreparing-to-use-umdh"></a><span id="preparing_to_use_umdh"></span><span id="PREPARING_TO_USE_UMDH"></span>准备使用 UMDH

如果尚未确定哪个进程正在泄漏内存，请先执行该操作。 有关详细信息，请参阅 [使用性能监视器查找内存泄漏 User-Mode](using-performance-monitor-to-find-a-user-mode-memory-leak.md)。

UMDH 日志中最重要的数据是堆分配的堆栈跟踪。 若要确定进程是否正在泄漏堆内存，请分析这些堆栈跟踪。

使用 UMDH 显示堆栈跟踪数据之前，必须使用 [GFlags](gflags.md) 正确配置系统。 GFlags 包含在 Windows 调试工具中。

以下 GFlags 设置启用 UMDH stack 跟踪：

-   在 GFlags 图形界面中，选择 "图像文件" 选项卡，键入进程名称 (包括文件扩展名) ，按 TAB 键，选择 " **创建用户模式堆栈跟踪数据库**"，然后选择 " **应用**"。

    或者，使用以下 GFlags 命令行，其中 *ImageName* 是进程名称 (包括文件扩展名) ：

    ```dbgcmd
    gflags /i ImageName +ust 
    ```
    完成后，使用此命令清除 GFlag 设置。 有关详细信息，请参阅 [GFlags 命令](gflags-commands.md)。

    ```dbgcmd
    gflags /i ImageName -ust 
    ```
    

-   默认情况下，在 x86 处理器上 Windows 收集的堆栈跟踪数据量限制为 32 MB，在 x64 处理器上限制为 64 MB。 如果必须增加此数据库的大小，请选择 "GFlags" 图形界面中的 " **映像文件** " 选项卡，键入进程名称，按 tab 键，选中 " **Stack Backtrace (Megs)** " 复选框，在 "关联" 文本框中键入值 (，以) MB 为单位），然后选择 " **应用**"。 仅在必要时增加此数据库，因为它可能会耗尽有限的 Windows 资源。 如果不再需要更大的大小，则将此设置返回到其原始值。

-   如果更改了 " **系统注册表** " 选项卡上的任何标志，则必须重新启动 Windows 才能使这些更改生效。 如果更改了 " **图像文件** " 选项卡上的任何标志，则必须重新启动该过程才能使更改生效。 对 **内核标志** 选项卡所做的更改将立即生效，但在下次重新启动 Windows 时，它们会丢失。

使用 UMDH 之前，必须有权访问应用程序的正确符号。 UMDH 使用环境变量 \_ NT 符号路径指定的符号路径 \_ \_ 。 将此变量设置为包含应用程序的符号的路径。 如果还包括 Windows 符号的路径，则分析可能更完整。 此符号路径的语法与调试器使用的语法相同;有关详细信息，请参阅 [符号路径](symbol-path.md)。

例如，如果你的应用程序的符号位于 C： \\ MySymbols，并且你想要为你的 Windows 符号使用公共 Microsoft 符号存储区，则使用 C： \\ MyCache 作为下游存储，你将使用以下命令设置你的符号路径：

```console
set _NT_SYMBOL_PATH=c:\mysymbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols 
```

此外，若要确保准确的结果，必须禁用 BSTR 缓存。 为此，请将 OANOCACHE 环境变量设置为等于 1)  (。 在启动要跟踪其分配的应用程序之前，请进行此设置。

如果需要跟踪服务所做的分配，则必须将 OANOCACHE 设置为系统环境变量，然后重新启动 Windows，使此设置生效。


### <a name="span-iddetecting_increases_in_heap_allocations_with_umdhspanspan-iddetecting_increases_in_heap_allocations_with_umdhspandetecting-increases-in-heap-allocations-with-umdh"></a><span id="detecting_increases_in_heap_allocations_with_umdh"></span><span id="DETECTING_INCREASES_IN_HEAP_ALLOCATIONS_WITH_UMDH"></span>检测通过 UMDH 增加的堆分配

进行这些准备后，可以使用 UMDH 捕获有关进程的堆分配的信息。 为此，请执行此过程：

1.  确定要调查的进程的 [进程 ID (PID) ](finding-the-process-id.md) 。

2.  使用 UMDH 分析此进程的堆内存分配，并将其保存到日志文件。 将-p 开关与 PID 一起使用，并将-f 开关与日志文件的名称一起使用。 例如，如果 PID 为124，并且你想要将日志文件命名 Log1.txt，请使用以下命令：

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

    对于每个调用堆栈 (在 UMDH 日志文件中标记为 "BackTrace" ) ，这两个日志文件之间有比较。 在此示例中，第一个日志文件 ( # A0) 记录为 BackTrace00B53 分配的0x9DF0 字节，而第二个日志文件记录了0xF110 字节，这意味着在捕获两个日志的时间之间分配了0x5320 个额外的字节。 这些字节来自 BackTrace00B53 标识的调用堆栈。

6.  若要确定该 backtrace 中的内容，请打开一个原始日志文件 (例如 Log2.txt) ，然后搜索 "BackTrace00B53"。 结果类似于以下数据：

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

    此 UMDH 输出显示有)  (十进制21280从调用堆栈中分配的总字节数。 这些字节是从 0x14 (十进制 20) 单独分配的，每个 0x428 (十进制 1064) 字节。

    将为调用堆栈提供 "BackTrace00B53" 的标识符，并显示此堆栈中的调用。 在检查调用堆栈时，可以看到 **DisplayMyGraphics** 例程正在通过 **new** 运算符分配内存，该运算符调用例程 *malloc*，后者使用 Visual C++ 运行时库从堆中获取内存。

    确定要在源代码中显式显示的最后一个调用。 在这种情况下，它可能是 **new** 运算符，因为调用 *malloc* 是作为 **新** 的实现的一部分而不是作为单独的分配。 因此， **DisplayMyGraphics** 例程中 **new** 运算符的此实例会重复分配未释放的内存。

 

 





