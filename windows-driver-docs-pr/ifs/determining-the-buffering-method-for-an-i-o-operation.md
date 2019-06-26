---
title: 确定 I/O 操作的缓冲方法
description: 确定 I/O 操作的缓冲方法
ms.assetid: 219378d9-a9fa-495a-b016-36595a7efb49
keywords:
- 缓冲区 WDK 文件系统微筛选器
- preoperation 回调例程 WDK 文件系统微筛选器，缓冲区
- postoperation 回调例程 WDK 文件系统微筛选器，缓冲区
- 缓冲的 I/O WDK 文件系统
- 直接 I/O WDK 文件系统
- 既不缓冲，也不直接 I/O WDK 文件系统
- 数据缓冲区 WDK 文件系统微筛选器
- I/O WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 184f6713ecc6e0acda8e01146e187ff4030d72a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386103"
---
# <a name="determining-the-buffering-method-for-an-io-operation"></a>确定 I/O 操作的缓冲方法


## <span id="ddk_determining_the_buffering_method_for_an_io_operation_if"></span><span id="DDK_DETERMINING_THE_BUFFERING_METHOD_FOR_AN_IO_OPERATION_IF"></span>


设备驱动程序，如文件系统负责用户模式应用程序和系统的设备之间传输数据。 操作系统提供了用于访问数据缓冲区的以下三种方法：

-   在中*缓冲 I/O*，I/O 管理器分配一个系统缓冲区，用于从非分页缓冲池执行的操作。 I/O 管理器将数据从该系统缓冲区复制到应用程序的用户缓冲区，反之亦然，启动 I/O 操作的线程的上下文中。

-   在中*直接 I/O*，I/O 管理器探测和锁定用户缓冲区。 然后，创建内存描述符列表 (MDL) 将映射锁定的缓冲区。 I/O 管理器访问启动 I/O 操作的线程的上下文中的缓冲区。

-   在中*既不缓冲，也不直接 I/O*，I/O 管理器不会分配一个系统缓冲并且不会锁定或映射用户缓冲区。 相反，它只是传递缓冲区的原始用户空间虚拟地址到文件系统堆栈。 驱动程序负责确保在启动线程的上下文中执行和缓冲区地址都有效。

    微筛选器驱动程序尝试使用它之前必须验证用户空间中的任何地址。 I/O 管理器和筛选器管理器不会验证此类地址，并不验证嵌入在传递给微筛选器驱动程序的缓冲区的指针。

所有标准 Microsoft 文件系统使用既不缓冲，也不直接 I/O，对于大多数 I/O 处理。

缓冲方法的详细信息，请参阅[方法的访问数据缓冲区](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。

对于基于 IRP 的 I/O 操作，使用的缓冲方法是特定于操作的并由以下因素决定：

-   正在执行的 I/O 操作的类型

-   值**标志**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)文件系统卷的结构

-   I/O 控制 (IOCTL) 和文件系统控制 (FSCTL) 操作的值*留空，则*参数传递给 CTL\_代码时 IOCTL 或 FSCTL 已定义的宏

快速的 I/O 操作始终具有缓冲区的使用都不缓冲也不直接 I/O。

文件系统回调操作不具有缓冲区。

本部分包括：

[可基于 IRP 的或快速 I/O 操作](operations-that-can-be-irp-based-or-fast-i-o.md)

[遵循设备对象标志的基于 IRP 的 I/O 操作](irp-based-i-o-operations-that-obey-device-object-flags.md)

[基于 IRP 的 I/O 操作始终使用缓冲的 I/O](irp-based-i-o-operations-that-always-use-buffered-i-o.md)

[基于 IRP 的 I/O 操作始终使用既不缓冲，也不直接 I/O](irp-based-i-o-operations-that-always-use-neither-buffered-nor-direct-i.md)

[基于 IRP 的 IOCTL 和 FSCTL 操作](irp-based-ioctl-and-fsctl-operations.md)

[有没有缓冲区的基于 IRP 的 I/O 操作](irp-based-i-o-operations-that-have-no-buffers.md)

 

 




