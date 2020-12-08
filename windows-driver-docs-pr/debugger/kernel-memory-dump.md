---
title: 内核内存转储
description: 内核内存转储
keywords:
- 转储文件，内核内存转储
- 内核内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cac742353c1eaa73cfb604a75387f822f5aacec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801917"
---
# <a name="kernel-memory-dump"></a>内核内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*内核内存转储* 包含发生崩溃时内核使用的所有内存。

此类转储文件明显小于完整内存转储。 通常，转储文件的大小为系统物理内存大小的三分之一。 此数量会因情况而异。

此转储文件将不包括未分配的内存或分配给用户模式应用程序的任何内存。 它仅包括分配给 Windows 内核和硬件抽象层 (HAL) ，以及分配给内核模式驱动程序和其他内核模式程序的内存。

大多数情况下，此故障转储最有用。 它比完整内存转储小得多，但它仅省略崩溃不太可能涉及的内存部分。

由于此类转储文件不包含任何在崩溃时驻留在内存中的用户模式可执行文件的映像，因此，如果这些可执行文件不重要，则可能还需要设置可执行映像路径。

默认情况下，内核内存转储文件写入% SystemRoot% \\ Memory。

如果发生第二次错误检查，并创建了另一个内核内存转储 (或完成内存转储) ，则将覆盖以前的文件。

若要在调试内核内存转储时取消丢失页错误消息，请使用 " [**忽略 \_ 缺少的 \_ 页**](-ignore-missing-pages--suppress-missing-page-errors-.md) " 命令。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

 

 






