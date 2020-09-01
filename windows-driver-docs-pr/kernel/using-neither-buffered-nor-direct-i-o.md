---
title: 既不使用缓冲 I/O，也不使用直接 I/O
description: 既不使用缓冲 I/O，也不使用直接 I/O
ms.assetid: e85af2e0-e532-47ca-918e-087e7aff859e
keywords:
- 缓冲 WDK i/o，无缓冲和直接 i/o
- 数据缓冲区 WDK i/o，无缓冲或直接 i/o
- 缓冲和直接 i/o WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab0e157cf2a8c0b71574cac47cd597b68ca2307
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190977"
---
# <a name="using-neither-buffered-nor-direct-io"></a>既不使用缓冲 I/O，也不使用直接 I/O





如果驱动程序使用的是非缓冲的，也不是直接 i/o，则 i/o 管理器会将其发送到驱动程序的 Irp 中的原始用户空间虚拟地址传递给它。 若要安全地访问这些缓冲区，驱动程序必须在调用线程的上下文中执行。 因此，通常只有最高级别的驱动程序（如 FSDs）可以使用此方法来访问缓冲区。

中间或最低级别的驱动程序无法始终满足此条件。 例如，如果请求线程等待 i/o 请求完成，或者如果高级驱动程序在中间或最低级别的驱动程序上分层，则不太可能在请求线程的上下文中调用低级驱动程序例程。

I/o 管理器确定 i/o 操作是不使用缓冲的，也不是直接 i/o，如下所示：

-   对于[**IRP \_ mj \_ 读取**](./irp-mj-read.md)和[**IRP \_ mj \_ 写入**](./irp-mj-write.md)请求，不 \_ \_ \_ \_ 会在[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**Flags**成员中设置缓冲 IO 和直接 IO。 有关详细信息，请参阅 [初始化设备对象](initializing-a-device-object.md)。

-   对于 [**IRP \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求，ioctl 代码的值都包含方法，而 \_ 不是作为 IOCTL 值中的 *TransferType* 值。 有关详细信息，请参阅 [定义 I/o 控制代码](defining-i-o-control-codes.md)。

当驱动程序收到一个 IRP，该 IRP 指定了不使用缓冲的 i/o 操作和直接 i/o 时，它必须执行以下操作：

1.  检查用户缓冲区的地址范围的有效性，并使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 和 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite) 支持例程检查是否允许相应的读取或写入访问。 驱动程序必须将其访问权限放入驱动程序提供的异常处理程序中的缓冲区的地址范围内，以便当驱动程序访问内存时，用户线程无法更改缓冲区的访问权限。 如果探测引发异常，驱动程序将返回错误。 驱动程序必须在发出 i/o 请求的线程的上下文中调用这些例程;因此，只有较高级别的驱动程序才能执行此任务。

2.  通过以下方式之一管理缓冲区和内存操作：
    -   执行其自己的双缓冲操作，因为 i/o 管理器对使用缓冲 i/o 的驱动程序进行处理。 有关详细信息，请参阅 [使用缓冲 i/o](using-buffered-i-o.md)。
    -   创建自己的 MDLs 并通过调用内存管理器的支持例程来锁定缓冲区，因为 i/o 管理器对使用直接 i/o 的驱动程序执行。 有关详细信息，请参阅 [使用直接 i/o](using-direct-i-o.md)。
    -   在调用线程的上下文中直接在用户缓冲区上执行所有必需的操作。 驱动程序必须在驱动程序提供的异常处理程序中包装其对缓冲区的访问权限，以防用户线程在驱动程序访问内存时更改缓冲区的访问权限或缓冲区中的数据。 有关详细信息，请参阅 [处理异常](handling-exceptions.md)。

实际上，驱动程序必须根据每个 IRP 来选择是否在调用线程的上下文中执行缓冲 i/o、直接 i/o 或 i/o，还必须处理用户模式线程上下文中可能发生的任何异常。 必要时，驱动程序必须管理自己的用户缓冲区访问、双缓冲操作和内存映射，而不是让 i/o 管理器处理驱动程序的这些操作。

 

