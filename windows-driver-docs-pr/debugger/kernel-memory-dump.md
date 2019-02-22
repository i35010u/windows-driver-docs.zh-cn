---
title: 内核内存转储
description: 内核内存转储
ms.assetid: 466f5b92-c9bd-4050-9ef8-469979ba0cbe
keywords:
- 转储文件中，内核内存转储
- 内核内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795d9129c45bdc39254e0a22a3cd3103fd4b8261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541652"
---
# <a name="kernel-memory-dump"></a>内核内存转储


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


一个*内核内存转储*包含在崩溃时内核使用的所有内存。

转储文件的此类型为显著小于完整内存转储。 通常情况下，转储文件将大约三分之一的系统上的物理内存大小。 此数量会相差很大，具体取决于您的环境。

此转储文件将包括未分配的内存或分配给用户模式应用程序的任何内存。 它只包括内存分配给 Windows 内核和硬件抽象层 (HAL)，以及分配给内核模式驱动程序和内核模式的其他程序的内存。

对于大多数情况下，此故障转储是最有用。 很明显短于完全内存转储，但它仅忽略不太可能已在发生崩溃中涉及的这些部分内存。

由于这种转储文件不包含任何在发生崩溃时驻留在内存中的用户模式下可执行文件的映像，可能还需要设置可执行映像路径，如果这些可执行文件最终并不重要。

内核内存转储文件写入到 %systemroot%\\Memory.dmp 默认情况下。

如果第二个 bug 检查发生，并且创建另一个内核内存转储 （以后或完全内存转储） 时，将覆盖以前的文件。

若要调试内核内存转储时，禁止显示缺失的页错误消息，请使用[ **.ignore\_缺少\_页**](-ignore-missing-pages--suppress-missing-page-errors-.md)命令。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

 

 






