---
title: 小规模内存转储
description: 小规模内存转储
keywords:
- 转储文件，小型内存转储
- 小规模内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f7f38b0d8e0f925bcfd3bef335358f6b0c89609
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795159"
---
# <a name="small-memory-dump"></a>小规模内存转储


## <span id="ddk_small_memory_dump_dbg"></span><span id="DDK_SMALL_MEMORY_DUMP_DBG"></span>


*小型内存转储* 比其他两种内核模式故障转储文件小很多。 它的大小恰好为 64 KB，只需要启动驱动器上的 64 KB 的页面文件空间。

此转储文件包含以下内容：

-   Bug 检查消息和参数以及其他蓝屏数据。

-   处理器上下文 (崩溃的处理器的 PRCB) 。

-   进程信息和内核上下文 (已崩溃的进程的 EPROCESS) 。

-   线程信息和内核上下文对于崩溃的线程 (ETHREAD) 。

-   损坏线程的内核模式调用堆栈。 如果此长度超过 16 KB，将仅包括最前面的 16 KB。

-   已加载的驱动程序的列表。

在 Windows XP 和更高版本的 Windows 中，还包括以下各项：

-   已加载模块和已卸载模块的列表。

-   调试器数据块。 这包含有关系统的基本调试信息。

-   Windows 标识为调试失败时可用的任何附加内存页。 这包括发生崩溃时寄存器指向的数据页，以及错误组件专门请求的其他页。

-    (Windows Server 2003 及更高版本) Windows SKU，例如 "专业" 或 "服务器"。

当空间大有限时，此类转储文件会很有用。 不过，由于包括的信息量有限，因此，在发生故障时不会直接导致的错误不会通过分析来发现。

由于此类转储文件在发生崩溃时不包含驻留在内存中的任何可执行文件的映像，因此，如果这些可执行文件非常重要，则可能还需要设置可执行映像路径。

如果发生第二个 bug 检查并创建了第二个小内存转储文件，则会保留上一个文件。 将为每个附加文件指定一个不同的名称，其中包含在文件名中编码的崩溃日期。 例如，mini022900-01 是在2000年2月29日生成的第一个内存转储文件。 目录% SystemRoot% 小型转储中保留了所有小内存转储文件的列表 \\ 。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

 

 






