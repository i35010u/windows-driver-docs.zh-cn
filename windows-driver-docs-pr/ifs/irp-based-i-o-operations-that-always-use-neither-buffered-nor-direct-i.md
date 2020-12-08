---
title: 不使用缓冲和直接 i/o 的 IRP-Based i/o 操作
description: 基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O
keywords:
- 缓冲和直接 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 667b6efc12b6cf3afe8df11fe720a96772441664
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830557"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


对于文件系统卷，以下基于 IRP 的 i/o 操作始终不使用缓冲和直接 i/o，无论 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的 **Flags** 成员值如何：

-   IRP\_MJ\_PNP

-   IRP \_ MJ \_ 查询 \_ 安全性

-   IRP \_ MJ \_ 设置 \_ 安全性

-   IRP\_MJ\_SYSTEM\_CONTROL

 

