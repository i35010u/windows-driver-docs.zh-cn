---
title: 内核模式转储文件的种类
description: 内核模式转储文件的种类
keywords:
- 转储文件，内核模式文件类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b74e6720426bb52f444523e0cf37084f5dcc5a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802979"
---
# <a name="varieties-of-kernel-mode-dump-files"></a>内核模式转储文件的种类


## <span id="ddk_varieties_of_kernel_mode_dump_files_dbg"></span><span id="DDK_VARIETIES_OF_KERNEL_MODE_DUMP_FILES_DBG"></span>


内核模式故障转储文件有五个设置：

[完整内存转储](complete-memory-dump.md)

[内核内存转储](kernel-memory-dump.md)

[小规模内存转储](small-memory-dump.md)

[自动内存转储](automatic-memory-dump.md)

[活动内存转储](active-memory-dump.md)

这些转储文件之间的差异是大小之一。 *完全内存转储* 是最大的，其中包含的信息最多，包括一些 User-Mode 内存。 *活动内存转储* 有些小，但对于大多数用途包含类似的信息。  *内核内存转储* 仍更小，通常会省略 User-Mode 内存，*小内存转储* 的大小仅为 64 KB。

如果选择 *自动内存转储*，则转储文件与内核内存转储相同，但 Windows 在设置系统分页文件的大小方面具有更大的灵活性。

较大的文件的优点是，由于它们包含更多的信息，因此它们更有可能帮助您找出崩溃的原因。

较小文件的优点是它们更小，编写得更快。 速度通常很有价值;如果你运行的是服务器，则可能希望服务器在崩溃后尽快重新启动，并且在写入转储文件之前不会进行重新启动。

创建完整的内存转储或内核内存转储后，可以从较大的转储文件创建小的内存转储文件。 有关详细信息，请参阅 [**dump (创建转储文件)**](-dump--create-dump-file-.md) 命令。

**注意**   通过分析内核模式转储文件，可以获得很多信息。 但是，任何内核模式转储文件都不能提供尽可能多的信息，因为它会直接与内核调试器直接调试故障。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件](kernel-mode-dump-files.md)

[启用内核模式转储文件](enabling-a-kernel-mode-dump-file.md)

 

 






