---
title: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
description: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
keywords:
- 缓冲 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bde923867b25697a9153eb544e62849349f78c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830565"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>基于 IRP 的 I/O 操作，始终使用缓冲的 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


以下基于 IRP 的 i/o 操作始终使用缓冲 i/o，而不考虑文件系统卷的 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的 **Flags** 成员值：

-   IRP \_ MJ \_ CREATE ([**EaBuffer 参数**](./flt-parameters-for-irp-mj-create.md)) 

-   IRP\_MJ\_QUERY\_INFORMATION

-   IRP \_ MJ \_ 查询 \_ 卷 \_ 信息

-   IRP\_MJ\_SET\_INFORMATION

-   IRP \_ MJ \_ 设置 \_ 卷 \_ 信息

请注意，IRP \_ MJ \_ 查询 \_ 信息还可以是一种快速的 i/o 操作。 当它是快速 i/o 操作时，它既不使用缓冲也不使用直接 i/o。 有关可以是基于 IRP 或快速 i/o 操作的 i/o 操作的详细信息，请参阅 [可 IRP-Based 或快速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o 的操作。

 

