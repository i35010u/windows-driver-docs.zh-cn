---
title: 类型的内核模式转储文件
description: 类型的内核模式转储文件
ms.assetid: 6db2a755-ed9c-492a-a650-9ae34ae59968
keywords:
- 转储文件中，内核模式下的文件类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f963d98be95c454f2be57cadbaaf792c09927e77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541019"
---
# <a name="varieties-of-kernel-mode-dump-files"></a>类型的内核模式转储文件


## <span id="ddk_varieties_of_kernel_mode_dump_files_dbg"></span><span id="DDK_VARIETIES_OF_KERNEL_MODE_DUMP_FILES_DBG"></span>


有五个设置内核模式崩溃转储文件：

[完全内存转储](complete-memory-dump.md)

[内核内存转储](kernel-memory-dump.md)

[小内存转储](small-memory-dump.md)

[自动内存转储](automatic-memory-dump.md)

[活动内存转储](active-memory-dump.md)

这些转储文件之间的差异是大小之一。 *完全内存转储*是最大，包含最多信息，包括一些用户模式内存。 *活动内存转储*值小一些，但大多数情况下包含类似的信息。  *内核内存转储*仍然是较小，通常省略用户模式内存中，并*小内存转储*是仅为 64 KB。

如果选择*自动内存转储*，转储文件等同于内核内存转储，但 Windows 对更灵活地设置系统分页文件的大小。

较大的文件的优点是，因为它们包含的详细信息，它们是更有可能帮助你找出崩溃的原因。

较小的文件的优点是它们是较小并将其写更快。 速度通常是有价值;如果正在运行一个服务器，可以将该服务器崩溃后尽快重新启动并重新启动将不会写入转储文件前发生。

创建完全内存转储或内核内存转储后，就可以从更大的转储文件创建一个小的内存转储文件。 请参阅[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)命令的详细信息。

**请注意**  多的信息可以通过分析内核模式转储文件。 但是，没有内核模式转储文件可以提供实际直接与内核调试程序调试崩溃尽可能多的信息。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[内核模式转储文件](kernel-mode-dump-files.md)

[启用内核模式转储文件](enabling-a-kernel-mode-dump-file.md)

 

 






