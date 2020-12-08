---
title: 解释日志比较结果
description: 解释日志比较结果
keywords:
- UMDH，解释日志比较
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e719e235cf1aaa811eb7494751169c05d7192d3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801959"
---
# <a name="interpreting-a-log-comparison"></a>解释日志比较结果


## <span id="ddk_interpreting_a_log_comparison_dtools"></span><span id="DDK_INTERPRETING_A_LOG_COMPARISON_DTOOLS"></span>


可以生成多个 User-Mode 转储堆 (在一段时间内 UMDH) 日志。 然后，可以使用 UMDH 比较日志，并确定哪些调用堆栈分配已在试验中增长最多。

例如，下面的命令指示 UMDH 比较两个 UMDH 日志、Log1.txt 和 Log2.txt，并将输出重定向到第三个文件，Compare.txt。

```console
umdh -v Log1.txt Log2.txt > Compare.txt
```

生成的 Compare.txt 文件将列出每个日志中记录的调用堆栈，并且对于每个堆栈，将显示日志文件之间堆分配中的更改。

例如，文件中的以下行显示了标记为 "Backtrace00053" 的调用堆栈中的函数分配大小更改。

在 Log1.txt 中，堆栈帐户中的调用 40432 (0x9DF0) 字节，但在 Log2.txt 中，同一调用堆栈帐户 61712 (0xF110) 个字节，两者的21280差异 () 个字节。

```console
+ 5320 (f110 - 9df0) 3a allocs BackTrace00053 
Total increase == 5320
```

下面是分配的堆栈：

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

调用堆栈的检查显示 **LeakyFunc** 函数正在使用 Visual C++ 运行时库分配内存。 如果对其他日志文件的检查显示分配随着时间的推移而增加，则可能会得出结论：从堆分配的内存未释放。

### <a name="span-idsymbol_files_for_analyzing_a_log_filespanspan-idsymbol_files_for_analyzing_a_log_filespanspan-idsymbol_files_for_analyzing_a_log_filespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>用于分析日志文件的符号文件

假设您有两台计算机：一 *台日志记录计算机* ，您可以在其中创建 UMDH 日志以及分析 UMDH 日志的 *分析计算机* 。 分析计算机上的符号路径必须指向在日志记录时日志记录计算机上加载的 Windows 版本的符号。 不要将分析计算机上的符号路径指向符号服务器。 如果这样做，UMDH 将检索分析计算机上运行的 Windows 版本的符号，UMDH 将不会显示有意义的结果。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[使用 UMDH 查找用户模式内存泄漏](using-umdh-to-find-a-user-mode-memory-leak.md)

 

 





