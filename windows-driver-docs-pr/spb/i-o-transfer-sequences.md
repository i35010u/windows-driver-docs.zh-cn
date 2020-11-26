---
title: I/O 传输序列
description: SPB 框架扩展 (SpbCx) 支持 i/o 传输顺序。
ms.assetid: 7415DB28-5E93-4F47-B169-7C652969D4C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5514bbd4497bb1a6e180f6b28d0b7ea97af2da3b
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157341"
---
# <a name="io-transfer-sequences"></a>I/O 传输序列

SPB 框架扩展 (SpbCx) 支持 i/o 传输顺序。 I/o 传输序列是一组有序的总线传输 (读取和写入操作，作为单个原子总线操作执行) 。 I/o 传输序列中的所有传输在总线上访问相同的目标设备。 执行序列时，即使在 i/o 传输序列完成之前，SPB 控制器驱动程序可能会收到其他设备的 i/o 请求，也无法访问总线上的其他设备。

I/o 传输序列的一个示例是一个写入读取操作，该操作是一个后跟总线读取操作的总线写入操作。 客户端外设驱动程序可以使用这种类型的序列来写入由 SPB 连接的外围设备中的函数选择注册，然后读取所选设备功能的值。 这两个传输的长度可能不同。 例如，写操作可能传输一个字节的数据，并且读取操作可能传输多个字节的数据。

## <a name="types-of-io-transfer-sequences"></a>I/o 传输序列的类型

客户端可以通过以下两种方式之一来启动 i/o 传输序列：

* 客户端可以在 [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) i/o 控制请求中指定整个序列。 此请求使 SPB 控制器驱动程序可以使用任何特定于硬件的性能优化来执行传输顺序。 有关详细信息，请参阅 [单请求序列](#single-request-sequences)。

* 客户端可以发送 [**ioctl \_ spb \_ 锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858) i/o 控制请求来在序列的开头锁定控制器，并在序列完成后发送 [**ioctl \_ spb \_ 解锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859) 。 锁定控制器时，客户端为序列中的每个读取或写入操作 ([**IRP \_ mj \_ 读取**](../kernel/irp-mj-read.md) 或 [**irp \_ mj \_ 写入**](../kernel/irp-mj-write.md)) 发送单独的 i/o 请求。 有关详细信息，请参阅 [客户端实现的序列](#client-implemented-sequences)。

只要有可能，客户端应使用 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求，此请求速度更快，不容易出错，并且大大减少了其他客户端被锁定在总线之外的时间。 不过，如果客户端必须查看序列中某个传输过程中读取的值，然后才能在序列中启动后续传输，则客户端可以使用 **ioctl \_ spb \_ 锁定 \_ 控制器** 和 **ioctl \_ spb \_ 解除 \_ 控制器** 请求。 在这种情况下，需要仔细设计，以避免在总线外锁定其他客户端的时间比所需时间更长，并且设计错误的外设驱动程序可能会降低整体系统性能。

## <a name="single-request-sequences"></a>Single-Request 序列

为了提高性能，SPB 控制器驱动程序应实现 [*EvtSpbControllerIoSequence*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence) 回调函数来处理 [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 请求。 此方法增加了对 SPB 控制器驱动程序的复杂性，但避免了在其他客户端被锁定在总线之外时，客户端将 i/o 传输序列作为一系列单独的读取和写入操作执行。

> [!NOTE]
> 强烈建议实现 *EvtSpbControllerIoSequence* 函数，这可能成为 Windows 8 的要求。

 传输序列的实现类似于简单的读取或写入操作，但此外还要求更新序列中单个传输之间的顺序操作的存储状态。 第一次传输完成后，SPB 控制器驱动程序会更新序列状态，以选择序列中的下一次传输。 序列状态存储在设备上下文中，并包含传递给 *EvtSpbControllerIoSequence* 回调的 [**SPBREQUEST**](./spbcx-object-handles.md)句柄。 SPB 控制器驱动程序使用此句柄获取顺序中单个传输的缓冲区、长度、方向和位置参数。 有关获取这些参数的详细信息，请参阅 [**SpbRequestGetTransferParameters**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)。

如果 SPB 控制器驱动程序无法执行所请求的 **IOCTL \_ SPB \_ 执行 \_ 顺序** 操作，它将使用失败代码完成该请求。 如果发生此类故障，客户端可以选择锁定总线，将 i/o 传输序列显式作为一系列简单的 i/o 请求，并将总线解锁。 有关详细信息，请参阅 [客户端实现的序列](#client-implemented-sequences)。

SpbCx 对 **IOCTL \_ SPB \_ * XXX*** 请求进行参数检查。 对于 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求，SpbCx 拒绝空序列和包含空缓冲区指针或长度为零的缓冲区的序列。

SPB 控制器驱动程序应验证序列中每个传输的长度是否不超过驱动程序指定的限制。 例如， (WDK) 的 Windows 驱动程序工具包中的 SkeletonI2C 示例驱动程序将无法执行指定传输超过4K 个字节的 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求，并将此请求的状态代码设置为 status \_ 无效 \_ 参数。 为 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求启动序列操作之前，驱动程序应该验证顺序中所有传输的参数，以验证是否可以成功完成操作。

SpbCx 绝不会在 *EvtSpbControllerIoSequence* 回调之前使用 [*EvtSpbControllerLock*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)回调，并且它永远不会跟随带有 [*EvtSpbControllerUnlock*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)回调的 *EvtSpbControllerIoSequence* 回调。

## <a name="client-implemented-sequences"></a>Client-Implemented 序列

SPB 控制器驱动程序的客户端可以将 i/o 传输序列显式执行为一系列简单的读取和写入操作。 客户端可以是内核模式驱动程序，也可以是控制连接到总线的外围设备的用户模式驱动程序。 在序列中第一次传输之前，客户端向目标设备发送 [**IOCTL \_ SPB \_ 锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858) 请求，以防在序列中的传输之间发生其他不相关的总线访问。 接下来，客户端发送 [**IRP \_ mj \_ 读取**](../kernel/irp-mj-read.md) 和 [**irp \_ mj \_ 写入**](../kernel/irp-mj-write.md) 请求以按顺序执行传输。 最后，客户端发送 [**IOCTL \_ SPB \_ UNLOCK \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859) 请求以释放锁定。

如果序列中的后续传输依赖于早期传输，则客户端可能需要实现此类型的 i/o 传输顺序。 例如，第一次读取可能指示以后要读取或写入的字节数。 但是，如果不存在这样的依赖项，则客户端应将 [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 请求发送到 SPB 控制器驱动程序，这可以更高效地执行序列。

在启动客户端实现的序列的 **ioctl \_ spb \_ 锁 \_ 控制器** 请求和结束序列的 **ioctl \_ spb \_ 解锁 \_ 控制器** 请求之间，客户端可以发送到目标设备的唯一 i/o 请求为 **IRP \_ mj \_ 读取** 和 **irp \_ mj \_ 写入** 请求。 任何违反此规则的情况都是错误。

SPB 锁仅用于保证读取和写入序列作为原子总线操作执行，应专门用于此目的。

有关详细信息，请参阅 [处理 Client-Implemented 序列](./handling-client-implemented-sequences.md)。
