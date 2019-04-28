---
title: 活动内存转储
description: 活动内存转储
ms.assetid: b40979b6-cd9a-4655-8030-8bde25d75113
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9f9f77986e00110db1338a7d8933a9e690d0e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354419"
---
# <a name="active-memory-dump"></a>活动内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*活动内存转储*类似于[完全内存转储](complete-memory-dump.md)，但筛选出不可能是与主机上的问题进行故障排除相关的页。 由于这种筛选，而是通常远远小于完全内存转储。 

此转储文件包括分配给用户模式应用程序的任何内存。 它还包括内存分配给 Windows 内核和硬件抽象层 (HAL)，以及分配给内核模式驱动程序和内核模式的其他程序的内存。 转储包括映射到内核或用户空间中的活动可用于调试，以及所选的页面文件支持的转换，待机，页面，如将内存分配与 VirtualAlloc 或页面文件的已修改页提供支持部分。 Active 转储不包括上可用的页面和清零的列表、 文件缓存，来宾 VM 页和各种其他类型的内存不可能在调试期间是有用的。 

Windows 托管虚拟机 (Vm) 时，活动内存转储是特别有用。 时采用完全内存转储，为每个 VM 的内容。 当存在多个 Vm 运行时，这可以考虑在主机系统上更大量的内存中使用。 很多时候，感兴趣的代码活动是父主机操作系统，不能在子 Vm 中。 活动内存转储筛选出与所有子 Vm 都关联的内存。 

活动内存转储文件写入到 %systemroot%\\Memory.dmp 默认情况下。

活动内存转储是在 Windows 10 中提供及更高版本。

**请注意**  若要调试活动的内存转储时，禁止显示缺失的页错误消息，请使用[ **.ignore\_缺少\_页**](-ignore-missing-pages--suppress-missing-page-errors-.md)命令。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

 

 






