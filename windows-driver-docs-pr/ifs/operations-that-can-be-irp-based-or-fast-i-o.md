---
title: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
description: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
keywords:
- fast i/o 缓冲 WDK 文件系统
- 标志成员 WDK 文件系统
- 设备对象标志 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8e91a2b9d28d5446ef5e987d7d8bb2812480cd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837779"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>操作，可以是基于 IRP 的操作或快速的 I/O 操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


以下类型的操作可以是基于 IRP 的操作，也可以是快速 i/o 操作：

-   IRP \_ MJ \_ 设备 \_ 控制。  (请注意，IRP \_ MJ \_ 内部 \_ 设备 \_ 控制始终基于 irp。 ) 

-   IRP \_ MJ \_ 查询 \_ 信息。 如果 **FileInformationClass** 参数为 **FileBasicInformation**、 **FileStandardInformation** 或 **FileNetworkOpenInformation**，此操作可为快速 i/o。

-   IRP \_ MJ \_ 读取。 微筛选器驱动程序可以 \_ \_ \_ \_ \_ 在 [**FLT \_ 操作 \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration) 结构中设置 FLTFL 操作注册 SKIP 缓存的 IO 标志，以避免接收快速 I/O IRP \_ MJ \_ 读取操作和缓存的基于 IRP 的读取。

-   IRP \_ MJ \_ 写入。 微筛选器驱动程序可以 \_ \_ \_ \_ \_ 在 FLT 操作注册结构中设置 FLTFL 操作注册 SKIP 缓存 IO 标记， \_ \_ 以避免接收快速 i/o IRP \_ MJ \_ 写入操作和缓存的基于 IRP 的写入。

当这些操作中的任何一种都是快速 i/o 操作时，它将始终不使用缓冲和直接 i/o，即使等效的基于 IRP 的操作使用不同的缓冲方法。

当 IRP \_ MJ \_ 设备 \_ 控件是快速 i/o 操作时，不管 IOCTL 的传输类型如何，它都始终使用未缓冲和直接的 i/o。

尽管 IRP \_ MJ \_ 锁定 \_ 控制可以是基于 IRP 或快速 i/o 操作的，但它没有缓冲区。

 

