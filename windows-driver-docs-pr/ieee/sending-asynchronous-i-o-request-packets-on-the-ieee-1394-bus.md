---
title: IEEE 1394 总线上发送的异步 I/O 请求数据包
description: IEEE 1394 总线上发送的异步 I/O 请求数据包
ms.assetid: 93ad0cdf-5ac2-4916-b90e-1e64ca4494b6
keywords:
- 发送异步 I/O 请求
- raw 模式寻址 WDK IEEE 1394 总线
- 虚拟模式寻址 WDK IEEE 1394 总线
- 正常模式寻址 WDK IEEE 1394 总线
- 解决了 WDK IEEE 1394 总线
- 数据块 WDK IEEE 1394 总线
- 连续数据块 WDK IEEE 1394 总线
- 非递增的数据块 WDK IEEE 1394 总线
- 缓冲区 WDK IEEE 1394 总线
- 总线重置生成 WDK IEEE 1394 总线
- 重置生成 WDK IEEE 1394 总线
- 锁定 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 900b3d0c4690d8f778ed42725fbc4a6e0b03365d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545631"
---
# <a name="sending-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>IEEE 1394 总线上发送的异步 I/O 请求数据包





驱动程序使用请求\_异步\_读取、 请求\_异步\_写入和请求\_异步\_锁发送异步读取、 写入和锁定到设备上的 IEEE 1394 总线的操作。 请求\_异步\_读取和请求\_异步\_编写，IRB 的特定于操作的参数存储在**u.AsyncRead**或**u.AsyncWrite** IRB 的成员。

### <a name="types-of-addressing"></a>寻址的类型

发出异步 I/O 请求的驱动程序必须指定类型的目标地址[ **IO\_地址**](https://msdn.microsoft.com/library/windows/hardware/ff537346)中**DestinationAddress** IRB 的成员。 目标地址由两个值组成： 节点地址和地址偏移量。 总线驱动程序为这两个值的解释取决于使用驱动程序的启动请求的寻址模式。

三种寻址模式是可用于发送异步 1394年数据包：*正常*，*原始*，并*虚拟*。

在正常模式寻址启动请求的驱动程序提供地址偏移量，但未指定目标设备的节点地址。 总线驱动程序将使用它存储在设备的 PDO 枚举设备时的信息的节点地址填充。

在原始的寻址模式下，启动请求的驱动程序必须提供的节点地址和地址偏移量。 此外，而不是将请求发送到目标设备的 PDO，驱动程序必须将发送请求到主控制器 PDO。 这会通知总线驱动程序，它不应覆盖数据包中的节点地址信息。

解决虚拟模式下，启动请求的驱动程序必须显式指示目标设备的数据包中的节点地址，就像在 raw 模式寻址一样。 虚拟设备没有实际节点地址 1394年总线上。 虚拟设备的节点地址是只是建立允许虚拟设备来标识其数据包的驱动程序的约定的值。 虚拟设备驱动程序时能正常运行，应收到所有数据包的总线上广播并筛查这些包，其中包含其设备的"节点地址。"的预先设定的值搜索

启动虚拟设备的请求的驱动程序不需要执行任何特殊步骤来阻止总线驱动程序覆盖记录的数据包中的节点地址。 当总线驱动程序第一次枚举虚拟设备时，它在设备的 PDO，该值指示虚拟设备的设备扩展中设置标志。 在接收到此设备的请求，总线驱动程序就能够确认它是虚拟设备，并且不会覆盖在包中的节点地址。

### <a name="buffering-of-io-requests"></a>缓冲的 I/O 请求

启动异步 I/O 请求的驱动程序必须向指定的 I/O 缓冲区 MDL 提供一个指针。 它将此指针放在**Mdl** IRB 的成员。 总线驱动程序使用此缓冲区以将其从该设备，或作为写入设备的数据源中读取的数据复制。

驱动程序指定中的数据缓冲区的大小**nNumberOfBytesToRead**或**nNumberOfBytesToWrite**的成员**u.AsyncXXX**，以及中的块大小**nBlockSize**成员。 事务实际发生时，总线驱动程序分解成数据包中指定的大小的数据**nBlockSize**。 默认情况下，总线驱动程序读取或连续将数据写入： 读取或写入到设备的地址空间中的后续位置的每个块。

下图说明了连续的数据块。

![说明连续数据块的关系图](images/1394blkd.png)

（可选） 该驱动程序可以指定异步\_标志\_NONINCREMENTING 标志请求; 然后总线驱动程序将为每个块使用相同的地址集。

下图演示了异步非递增的数据块。

![说明异步非递增的数据块的关系图](images/1394blkf.png)

**警告**  总线驱动程序强制实施设备和计算机之间的当前连接速度的最大异步数据包大小和最大值中报告设备的最大速度\_REC 字段及其配置 rom。 如果**nBlockSize**是大于这些值，总线驱动程序所使用的块大小的强制的值。 如果驱动程序设置异步\_标志\_NONINCREMENTING 标志，这是不可能提供所需的行为。 如果驱动程序设置此标志，它们应检查提交请求之前的块大小是否小于已强制实施限制。

 

### <a name="sending-lock-requests"></a>发送锁请求

IEEE 1394 总线协议提供了异步锁定请求，它允许原子、 测试和集类型的操作。 除了指定的目标地址 (在**u.AsyncLock.DestinationAddress**)，该驱动程序指定的事务类型 (在**u.AsyncLock.fulTransactionType**)。 （请参阅详细信息的 IEEE 1394 规范） 中传递的数据值和操作的参数值**u.AsyncLock.DataValues**并**u.AsyncLock.Arguments**。

### <a name="bus-reset-generation"></a>总线重置生成

使用异步 I/O 的设备驱动程序跟踪的总线重置生成。 在每个异步请求的设备驱动程序报告中的该值**u.AsyncXxx.ulGeneration**请求 IRB 的成员。 总线驱动程序将到实际生成计数的值进行比较并如果它们无法与匹配，状态将 status 值使请求失败\_无效\_生成。 如果某个请求失败这种方式，该驱动程序应正确生成使用查询的请求\_获取\_代\_计数总线请求。 但是，该驱动程序应不重新发出任何请求都失败，此状态，直到它检索其总线重置通知回调中的新生成。 这可确保设备在总线上仍然存在。 请注意，客户端驱动程序不应依赖于 IRP\_MN\_总线\_重置总线重置操作的通知。 IRP\_MN\_总线\_重置是 Windows XP 和更高版本操作系统中已过时。

 

 




