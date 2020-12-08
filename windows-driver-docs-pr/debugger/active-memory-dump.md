---
title: 活动内存转储
description: 活动内存转储
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd3f5bed0264d52031339e6428f505afbf530932
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796295"
---
# <a name="active-memory-dump"></a>活动内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*活动内存转储* 类似于 [完整的内存转储](complete-memory-dump.md)，但它会筛选出不可能与解决主机上的问题相关的页面。 由于这种筛选，通常比完整的内存转储小得多。 

此转储文件包含分配给用户模式应用程序的任何内存。 它还包括分配给 Windows 内核和硬件抽象层 (HAL) ，以及分配给内核模式驱动程序和其他内核模式程序的内存。 转储包含映射到内核或用户空间的活动页面，这些页面可用于调试，以及所选页面文件支持的转换、备用和已修改的页面，例如通过 VirtualAlloc 或页面文件支持的部分分配的内存。 活动转储不包括免费和零个列表中的页面、文件缓存、来宾 VM 页面以及在调试过程中不可能有用的各种其他类型的内存。 

当 Windows 承载 (Vm) 的虚拟机时，活动内存转储特别有用。 在获取完整内存转储时，将包括每个 VM 的内容。 当有多个 Vm 正在运行时，这可能会占用主机系统上的大量内存。 很多情况下，相关的代码活动位于父主机操作系统中，而不是子 Vm。 活动内存转储筛选出与所有子 Vm 关联的内存。 

默认情况下，将活动内存转储文件写入% SystemRoot% \\ Memory。

活动内存转储在 Windows 10 和更高版本中可用。

**注意**  若要在调试活动内存转储时取消丢失页错误消息，请使用 " [**忽略 \_ 缺少的 \_ 页**](-ignore-missing-pages--suppress-missing-page-errors-.md) " 命令。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

 

 






