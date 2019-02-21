---
title: 解释日志比较
description: 解释日志比较
ms.assetid: fe2acdd5-00aa-4414-a59e-e6203ad48363
keywords:
- UMDH，解释日志比较
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f223dab0c0d50915f715758a9302b53f6deb87b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543833"
---
# <a name="interpreting-a-log-comparison"></a>解释日志比较


## <span id="ddk_interpreting_a_log_comparison_dtools"></span><span id="DDK_INTERPRETING_A_LOG_COMPARISON_DTOOLS"></span>


随着时间的推移，你可以生成多个用户模式转储堆 (UMDH) 日志在相同的过程。 然后，可以使用 UMDH 比较日志，并确定哪些调用堆栈分配一代代产品的试用版之间最多。

例如，以下命令将定向 UMDH 来比较两个 UMDH 日志，Log1.txt 和 Log2.txt，并将输出重定向到第三个文件，Compare.txt。

```console
umdh -v Log1.txt Log2.txt > Compare.txt
```

生成的 Compare.txt 文件列出每个日志中记录的调用堆栈，并为每个堆栈显示中的日志文件之间的堆分配的变化。

例如，文件中的以下行显示更改了中标记为"Backtrace00053。"的调用堆栈中的函数的分配大小

Log1.txt，在调用堆栈中的帐户 40,432 (0x9DF0) 个字节，但在 Log2.txt，相同的调用堆栈的帐户 61,712 (0xF110) 个字节，差值为 21,280 (0x5320) 字节。

```console
+ 5320 (f110 - 9df0) 3a allocs BackTrace00053 
Total increase == 5320
```

以下是用于分配的堆栈：

```console
ntdll!RtlDebugAllocateHeap+0x000000FD
ntdll!RtlAllocateHeapSlowly+0x0000005A
ntdll!RtlAllocateHeap+0x00000808
MyApp!_heap_alloc_base+0x00000069
MyApp!_heap_alloc_dbg+0x000001A2
MyApp!_nh_malloc_dbg+0x00000023
MyApp!_nh_malloc+0x00000016
MyApp!operator new+0x0000000E
MyApp!LeakyFunc+0x0000001E
MyApp!main+0x0000002C
MyApp!mainCRTStartup+0x000000FC
KERNEL32!BaseProcessStart+0x0000003D
```

检查调用堆栈显示**LeakyFunc**函数通过使用 Visual c + + 运行时库分配内存。 如果检查其他日志文件显示随着时间逐渐分配，你可能能够得出结论： 从堆中分配的内存不被释放。

### <a name="span-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>用于分析日志文件的符号文件

假设您有两台计算机：*记录计算机*创建 UMDH 日志以及一个*分析计算机*分析 UMDH 日志的位置。 分析计算机上的符号路径必须指向日志时间在加载日志记录计算机的 Windows 版本的符号。 未指向符号路径分析计算机上的符号服务器。 如果这样做，UMDH 将检索分析计算机运行的 Windows 版本的符号和 UMDH 将不会显示有意义的结果。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[使用 UMDH 来查找用户模式内存泄漏](using-umdh-to-find-a-user-mode-memory-leak.md)

 

 





