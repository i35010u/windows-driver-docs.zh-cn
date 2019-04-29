---
title: 小规模内存转储
description: 小规模内存转储
ms.assetid: bc502411-5366-49d3-b650-9dddda286934
keywords:
- 转储文件，小内存转储
- 小规模内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e7d9533432a68881b66c4ae9f99d18d8c7bfaff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368439"
---
# <a name="small-memory-dump"></a>小规模内存转储


## <span id="ddk_small_memory_dump_dbg"></span><span id="DDK_SMALL_MEMORY_DUMP_DBG"></span>


一个*小内存转储*比其他两种类型的内核模式崩溃转储文件小得多。 它是完全 64 KB 的大小，并且需要仅 64 KB 的启动驱动器上的页面文件空间。

此转储文件包含下列内容：

-   Bug 检查消息和参数，以及其他蓝屏的数据。

-   崩溃的处理器的处理器上下文 (PRCB)。

-   进程信息和内核上下文 (EPROCESS) 的进程的崩溃。

-   线程的信息和内核上下文 (ETHREAD) 的线程的崩溃。

-   内核模式崩溃的线程调用堆栈。 如果这是超过 16 KB，将包含仅最顶层的 16 KB。

-   加载的驱动程序列表。

在 Windows XP 和更高版本的 Windows 中，要还包含以下项：

-   已加载的模块和卸载的模块的列表。

-   调试器数据块。 其中包含有关系统的基本调试信息。

-   Windows 识别为用于调试失败的任何额外的内存页。 这包括出现故障时，寄存器都指向数据页和出错的组件专门请求其他页。

-   (Windows Server 2003 及更高版本)Windows SKU-例如，"专业"或"服务器"。

空间极大地限制时，此类型的转储文件非常有用。 但是，由于有限数量的包含的信息，直接不由在崩溃时执行的线程导致的错误可能不会发现此文件进行分析。

由于这种转储文件不包含任何可执行文件，在发生崩溃时驻留在内存中的映像，可能还需要设置的可执行映像路径，如果这些可执行文件最终并不重要。

如果将第二个进行错误检查，并创建第二个小内存转储文件，将保留以前的文件。 每个其他文件都有不同的名称，其中包含在文件名中编码在发生崩溃的日期。 例如，mini022900 01.dmp 是在 2000 年 2 月 29 日上生成的第一个内存转储文件。 所有小内存转储文件的列表保存在目录 %systemroot%\\小型转储。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

 

 






