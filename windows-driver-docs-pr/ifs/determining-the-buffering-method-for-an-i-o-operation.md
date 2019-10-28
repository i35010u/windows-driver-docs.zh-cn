---
title: 确定 I/O 操作的缓冲方法
description: 确定 I/O 操作的缓冲方法
ms.assetid: 219378d9-a9fa-495a-b016-36595a7efb49
keywords:
- 缓冲 WDK 文件系统微筛选器
- preoperation 回调例程 WDK 文件系统微筛选器，缓冲区
- postoperation 回调例程 WDK 文件系统微筛选器，缓冲区
- 缓冲 i/o WDK 文件系统
- 直接 i/o WDK 文件系统
- 缓冲和直接 i/o WDK 文件系统
- 数据缓冲区 WDK 文件系统微筛选器
- I/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb544b5f22bd583ec458fddd24ecd0744d83f05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841438"
---
# <a name="determining-the-buffering-method-for-an-io-operation"></a>确定 I/O 操作的缓冲方法


## <span id="ddk_determining_the_buffering_method_for_an_io_operation_if"></span><span id="DDK_DETERMINING_THE_BUFFERING_METHOD_FOR_AN_IO_OPERATION_IF"></span>


与设备驱动程序一样，文件系统负责在用户模式应用程序和系统设备之间传输数据。 操作系统提供以下三种方法来访问数据缓冲区：

-   在*缓冲 i/o*中，i/o 管理器从非分页池为操作分配系统缓冲区。 I/o 管理器将数据从该系统缓冲区复制到应用程序的用户缓冲区中，反之亦然，在启动 i/o 操作的线程的上下文中。

-   在*直接 i/o*中，i/o 管理器探测并锁定用户缓冲区。 然后，它创建内存描述符列表（MDL）来映射锁定缓冲区。 I/o 管理器在启动 i/o 操作的线程的上下文中访问缓冲区。

-   在未*缓冲或直接*i/o 的情况下，i/o 管理器不会分配系统缓冲区，也不会锁定或映射用户缓冲区。 相反，它只是将缓冲区的原始用户空间虚拟地址传递到文件系统堆栈。 驱动程序负责确保它们在启动线程的上下文中执行，并且缓冲区地址有效。

    微筛选器驱动程序必须先验证用户空间中的任何地址，然后才能尝试使用它。 I/o 管理器和筛选器管理器不会验证此类地址，也不会验证已传递给微筛选器驱动程序的缓冲区中嵌入的指针。

所有标准的 Microsoft 文件系统都不会对大多数 i/o 处理使用缓冲和直接 i/o。

有关缓冲方法的详细信息，请参阅[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。

对于基于 IRP 的 i/o 操作，使用的缓冲方法是特定于操作的，并由以下因素决定：

-   正在执行的 i/o 操作的类型

-   设备的**Flags**成员的值\_文件系统卷的[**对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构

-   对于 i/o 控制（IOCTL）和文件系统控制（FSCTL）操作，定义 IOCTL 或 FSCTL 后传递到 CTL\_代码宏的*TransferType*参数的值

具有缓冲区的快速 i/o 操作始终不使用缓冲和直接 i/o。

文件系统回调操作没有缓冲区。

本部分包括：

[可以是基于 IRP 或快速 i/o 的操作](operations-that-can-be-irp-based-or-fast-i-o.md)

[遵循设备对象标志的基于 IRP 的 i/o 操作](irp-based-i-o-operations-that-obey-device-object-flags.md)

[始终使用缓冲 i/o 的基于 IRP 的 i/o 操作](irp-based-i-o-operations-that-always-use-buffered-i-o.md)

[基于 IRP 的 i/o 操作，这些操作始终不使用缓冲和直接 i/o](irp-based-i-o-operations-that-always-use-neither-buffered-nor-direct-i.md)

[基于 IRP 的 IOCTL 和 FSCTL 操作](irp-based-ioctl-and-fsctl-operations.md)

[没有缓冲区的基于 IRP 的 i/o 操作](irp-based-i-o-operations-that-have-no-buffers.md)

 

 




