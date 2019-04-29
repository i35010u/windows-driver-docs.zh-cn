---
title: 支持 IEEE 1394 虚拟设备驱动程序中的请求
description: 支持 IEEE 1394 虚拟设备驱动程序中的请求
ms.assetid: 17e0c84b-29d9-461f-a5f6-7677ecb7fb6e
keywords:
- 仿真驱动程序 WDK IEEE 1394 总线
- 硬件仿真驱动程序 WDK IEEE 1394 总线
- 虚拟设备 WDK IEEE 1394 总线
- REQUEST_ASYNC_READ
- REQUEST_ASYNC_WRITE
- REQUEST_ASYNC_LOCK
- REQUEST_ALLOCATE_ADDRESS_RANGE
- REQUEST_GET_ADDR_FROM_DEVICE_OBJECT
- REQUEST_SET_DEVICE_XMIT_PROPERTIES
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30ddcd8bcf65daec9dcd058ec871f899d69ab8f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390308"
---
# <a name="supporting-requests-in-ieee-1394-virtual-device-drivers"></a>支持 IEEE 1394 虚拟设备驱动程序中的请求





虚拟 PDOs 和加载其上方的驱动程序具有的访问权限到实际的硬件的 1394年总线 DDI 功能驱动程序加载 PDO 上具有相同的级别。 但是，由于没有任何实际硬件，也在虚拟驱动程序的情况下，1394年总线驱动程序必须视为某些请求特殊情况。 本主题介绍如果发往虚拟 PDO 表现出不同的行为的请求：

-   [**请求\_异步\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff537634)， [**请求\_异步\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff537636)，和[ **请求\_异步\_锁**](https://msdn.microsoft.com/library/windows/hardware/ff537633)

    通常情况下，当应用程序或驱动程序地址的目标设备的异步 I/O 请求，1394年总线驱动程序从设备的物理设备对象 (PDO) 设备扩展提取设备的节点 ID。 当枚举设备时，将设备的 PDO 扩展中记录此信息。 虚拟设备，但是，不是枚举以通常的方式，因此生成请求的驱动程序*必须*提供的一个节点 ID，将请求发送到虚拟设备时就像它像执行异步 I/O 在 raw 模式中的一样。 Raw 模式寻址的讨论，请参阅[发送异步 I/O 请求数据包上的 IEEE 1394 总线](https://msdn.microsoft.com/library/windows/hardware/ff538087)。

    当总线驱动程序收到请求时对虚拟设备的 PDO 时，它使用提供的发起请求的驱动程序，而不是尝试的节点 ID 从设备扩展中提取的节点 ID。 严格地说，虚拟设备不具有节点的 Id，因此，将请求发送到虚拟设备的驱动程序必须提供一个备用节点 id。 按照约定，虚拟设备使用 PC 的主控制器的节点 ID。

    虚拟设备的驱动程序分配内存，它指定它将接收广播 1394年总线的所有数据包。 然后，驱动程序通过检查收到的每个数据包中的主机控制器的节点 ID 来标识其数据包。

    虚拟设备没有数据包大小或传输速率信息记录在其设备扩展，因为它们是硬件参数。 对于虚拟设备，总线驱动程序使用数据包大小和传输速率的信息已存储在该端口的设备对象中。

-   [**请求\_分配\_地址\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff537632)

    虚拟设备的驱动程序的访问权限必须设置\_标志\_类型\_广播中的标志**fulAccessType** IRB 通过请求分配内存时的成员\_分配\_地址\_范围请求。 由于虚拟设备有没有实际的节点编号，虚拟设备的驱动程序有接收请求，除非它们在广播模式下接收数据包的任何方法。 如果多个节点均分配相同的地址范围，只有一个将接收发往该范围内的异步请求。 如果虚拟设备和物理设备驱动程序分配相同的地址范围，物理设备的优先级高于虚拟设备，并因此物理设备接收数据包。 如果多个虚拟设备分配相同的地址范围，以分配范围的第一个驱动程序将具有优先级。

-   [**REQUEST\_GET\_ADDR\_FROM\_DEVICE\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff537641)

    虚拟设备具有没有相应的硬件节点和其自己的任何节点 ID。 虚拟设备驱动程序返回在总线上的主控制器在收到此请求时的节点 ID 而不是物理节点的节点 ID。

-   [**REQUEST\_SET\_DEVICE\_XMIT\_PROPERTIES**](https://msdn.microsoft.com/library/windows/hardware/ff537662)

    此请求不是支持虚拟设备因为没有相应的硬件节点从其获取节点 id。

对于所有其他请求，虚拟和物理设备之间的行为是相同的。

 

 




