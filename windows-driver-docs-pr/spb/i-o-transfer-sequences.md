---
title: I/O 传输序列
description: 存储框架扩展 (SpbCx) 支持 I/O 传输序列。
ms.assetid: 7415DB28-5E93-4F47-B169-7C652969D4C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffbe0d3ea5c54f3185f321dd0e85df598e0bb63c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356711"
---
# <a name="io-transfer-sequences"></a>I/O 传输序列


存储框架扩展 (SpbCx) 支持 I/O 传输序列。 I/O 传输序列是一组有序的总线传输 （读取和写入操作），作为单个、 原子总线操作执行。 在 I/O 传输序列中传输的所有访问总线上相同的目标设备。 一个序列，在执行时，可以访问总线上的没有其他设备，即使存储控制器驱动程序可能会收到其他设备的 I/O 请求 I/O 传输序列完成之前也是如此。

I/O 传输序列的示例是一个读写操作，这是读取操作的总线后, 跟一个总线写操作。 客户端外围设备驱动程序可能会使用此类型的序列将写入存储连接的外围设备中的函数选择寄存器，然后阅读所选的设备函数的值。 不同长度可以是以下两个传输。 例如，写入操作可能会传输一个字节的数据，并且读取的操作可能会传输数据的字节数。

## <a name="types-of-io-transfer-sequences"></a>类型的 I/O 传输序列


客户端可以启动 I/O 传输序列中通过以下两种方法之一：

-   客户端可以指定中的整个序列[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 控制请求。 此请求启用存储控制器驱动程序使用任何特定于硬件的性能优化，可用于执行传输序列。 有关详细信息，请参阅[单请求序列](#buses-single-request-sequences)。

-   客户端可以发送[ **IOCTL\_存储\_锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858) I/O 控制请求锁定在序列开头的控制器并发送[ **IOCTL\_存储\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)序列何时完成。 当控制器处于锁定状态时，客户端发送一个单独的 I/O 请求 ([**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)或者[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)) 为每个读取或写入操作的顺序。 有关详细信息，请参阅[Client-Implemented 序列](#buses-client-implemented-sequences)。

只要有可能，应使用客户端**IOCTL\_存储\_EXECUTE\_序列**请求，这是速度更快，不太容易发生错误，并明显减少在的其他过程的时间客户端被锁定在总线之外。 但是，可以使用客户端**IOCTL\_存储\_锁\_控制器**并**IOCTL\_存储\_解锁\_控制器**请求如果它必须查看之前它可以启动序列中的更高版本复制期间其中一个传输序列中读取的值。 在这种情况下，精心的设计是避免锁定超出的总线长于是必需的其他客户端所必需的设计得不合理的外围设备驱动程序会降低总体系统性能。

## <a name="single-request-sequences"></a>单请求序列


若要提高性能，您的存储控制器驱动程序应实现[ *EvtSpbControllerIoSequence* ](https://msdn.microsoft.com/library/windows/hardware/hh450810)回调函数来处理[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求。 这种方法向存储控制器驱动程序添加某种程度的复杂性，但可以避免需要客户端来执行 I/O 传输序列作为一系列单独读取和写入操作，而其他客户端被锁定在总线。

**请注意**  的实现*EvtSpbControllerIoSequence*函数强烈建议，并可能会针对 Windows 8 的一项要求。

 

传输序列的实现类似于简单的读取或写入操作，但此外要求对序列中的各个传输之间的序列操作的存储状态的更新。 首次传输完成后，存储控制器驱动程序更新要选择下一个传输序列中的序列状态。 序列状态存储在设备上下文中，包括[ **SPBREQUEST** ](https://msdn.microsoft.com/library/windows/hardware/hh450925)句柄传递给*EvtSpbControllerIoSequence*回调。 存储控制器驱动程序使用此句柄来获取缓冲区、 长度、 方向，并为序列中的各个传输位置参数。 有关获取这些参数的详细信息，请参阅[ **SpbRequestGetTransferParameters**](https://msdn.microsoft.com/library/windows/hardware/hh450924)。

如果存储控制器驱动程序将无法执行请求**IOCTL\_存储\_EXECUTE\_序列**操作，完成了失败代码的请求。 如果发生此类故障，客户端可以作为一个选项，锁定总线、 明确地执行 I/O 传输序列作为一系列简单的 I/O 请求，然后解锁总线。 有关详细信息，请参阅[Client-Implemented 序列](#buses-client-implemented-sequences)。

SpbCx does 参数检查**IOCTL\_存储\_* XXX*** 从外围设备驱动程序收到的请求。 有关**IOCTL\_存储\_EXECUTE\_序列**请求时，SpbCx 拒绝空序列和包含缓冲区指针为 NULL 或零长度的缓冲区的序列。

存储控制器驱动程序应验证序列中每次传输的长度不超过驱动程序指定的限制。 例如，SkeletonI2C 示例驱动程序 Windows Driver Kit (WDK) 中失败**IOCTL\_存储\_EXECUTE\_序列**指定超过 4k 字节的传输和设置状态的请求此请求状态代码\_无效\_参数。 初始化为序列操作之前**IOCTL\_存储\_EXECUTE\_序列**请求，驱动程序应验证所有传输序列中，若要验证的参数可以成功完成操作。

永远不会位于 SpbCx *EvtSpbControllerIoSequence*具有回调[ *EvtSpbControllerLock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)回调，并且它永远不会遵循*EvtSpbControllerIoSequence*具有回调[ *EvtSpbControllerUnlock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)回调。

## <a name="client-implemented-sequences"></a>客户端实现序列


存储控制器驱动程序的客户端可以显式执行 I/O 传输序列，如一系列简单的读取和写入。 客户端可以是一个内核模式驱动程序或控制连接到总线的外围设备的用户模式驱动程序。 之前在序列中第一个传输，客户端发送[ **IOCTL\_存储\_锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)到目标设备的请求，以防止其他，从出现的顺序传输之间的不相关的总线访问。 接下来，客户端发送[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)按顺序执行传输的请求。 最后，客户端发送[ **IOCTL\_存储\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)释放锁的请求。

客户端可能需要实施这种类型的 I/O 传输序列，如果序列中的更高版本传输程序依赖于早期的传输。 例如，第一次读取可能指示更多的字节数，随后读取或写入。 如果没有此类依赖项存在，但是，客户端应发送[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求存储控制器驱动程序，后者可以更有效地执行序列。

之间**IOCTL\_存储\_锁\_控制器**请求启动客户端实现的序列，和**IOCTL\_存储\_解锁\_控制器**结束序列，请求客户端可以发送到目标设备的唯一 I/O 请求**IRP\_MJ\_读取**和**IRP\_MJ\_编写**请求。 此规则的任何冲突时出错。

存储锁仅用于保证读取和写入一系列作为总线原子操作，执行，并应专门用于此目的。

有关详细信息，请参阅[Handling Client-Implemented 序列](https://msdn.microsoft.com/library/windows/hardware/jj191736)。

 

 




