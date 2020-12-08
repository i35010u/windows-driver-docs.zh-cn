---
title: 完整内存转储
description: 完整内存转储
keywords:
- 转储文件，完整内存转储
- 完整内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d68ae2afb8bbbbb116989fccb3cc097b9aafbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831957"
---
# <a name="complete-memory-dump"></a>完整内存转储


## <span id="ddk_complete_memory_dump_dbg"></span><span id="DDK_COMPLETE_MEMORY_DUMP_DBG"></span>


*完全内存转储* 是最大的内核模式转储文件。 此文件包含 Windows 使用的所有物理内存。 默认情况下，完全内存转储不包括平台固件使用的物理内存。

从 Windows 8 开始，可以注册在完整内存转储过程中调用的 [*BugCheckAddPagesCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine) 例程。 *BugCheckAddPagesCallback* 例程可以指定要添加到转储文件的特定于驱动程序的数据。 例如，这些附加数据可能包括未映射到虚拟内存中的系统地址范围的物理页面，但包含有助于调试驱动程序的信息。 *BugCheckAddPagesCallback* 例程可能会向转储文件添加未映射的任何驱动程序拥有的物理页面，或映射到虚拟内存中的用户模式地址的任何驱动程序。

此转储文件要求启动驱动器上的页面文件大小至少与主系统内存相同;它应该能够容纳大小等于整个 RAM 和 1 mb 的文件。

默认情况下，将完整的内存转储文件写入% SystemRoot% \\ Memory。

如果发生第二次错误检查，并创建了另一个完整的内存转储 (或内核内存转储) ，则将覆盖以前的文件。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

 

