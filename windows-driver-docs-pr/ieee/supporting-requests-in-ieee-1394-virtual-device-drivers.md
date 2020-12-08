---
title: 支持 IEEE 1394 虚拟设备驱动程序中的请求
description: 支持 IEEE 1394 虚拟设备驱动程序中的请求
keywords:
- 模拟驱动程序 WDK IEEE 1394 总线
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
ms.openlocfilehash: d08258db295feaedd3e89978ce8c4f554f81b93d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815405"
---
# <a name="supporting-requests-in-ieee-1394-virtual-device-drivers"></a>支持 IEEE 1394 虚拟设备驱动程序中的请求





虚拟 PDOs 和加载到其上面的驱动程序具有对1394总线 DDI 的相同级别的访问权限，而在 PDO 上加载的功能性驱动程序必须是实际硬件。 不过，由于虚拟驱动程序没有实际硬件，1394总线驱动程序必须将某些请求视为特殊情况。 本主题介绍在处理虚拟 PDO 时表现出不同行为的请求：

-   [**请求 \_ASYNC \_ READ**](https://msdn.microsoft.com/library/windows/hardware/ff537634)， [**请求 \_ 异步 \_ 写入**](https://msdn.microsoft.com/library/windows/hardware/ff537636)，并 [**请求 \_ async \_ LOCK**](https://msdn.microsoft.com/library/windows/hardware/ff537633)

    通常情况下，当应用程序或驱动程序对目标设备的异步 i/o 请求进行寻址时，1394总线驱动程序将从设备的物理设备对象的设备扩展中提取设备的节点 ID， (PDO) 。 枚举设备后，此信息会记录在设备的 PDO 扩展中。 不过，虚拟设备不是以常规方式进行枚举的，因此，生成请求的驱动程序在向虚拟设备发送请求时 *必须* 提供节点 ID，就像在 raw 模式下执行异步 i/o 一样。 有关 raw 模式寻址的讨论，请参阅 [在 IEEE 1394 总线上发送异步 I/o 请求数据包](./sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus.md)。

    当总线驱动程序收到虚拟设备的 PDO 请求时，它将使用发出请求的驱动程序提供的节点 ID，而不是尝试从设备扩展中提取节点 ID。 严格地说，虚拟设备没有节点 Id，因此向虚拟设备发送请求的驱动程序必须提供备用节点 ID。 按照约定，虚拟设备使用电脑的主机控制器的节点 ID。

    当虚拟设备的驱动程序分配内存时，它会指定它将接收在1394总线上广播的所有数据包。 然后，该驱动程序通过在它所接收的每个数据包中检查主机控制器的节点 ID 来识别其数据包。

    虚拟设备不会记录在其设备扩展中的数据包大小或传输速率信息，因为这些是硬件参数。 对于虚拟设备，总线驱动程序使用存储在端口的设备对象中的数据包大小和传输速率信息。

-   [**请求 \_ 分配 \_ 地址 \_ 范围**](https://msdn.microsoft.com/library/windows/hardware/ff537632)

    虚拟设备的驱动程序必须在 \_ \_ \_ 通过 **fulAccessType** 请求 \_ 分配 \_ 地址范围请求分配内存时，在 IRB 的 fulAccessType 成员中设置访问标志类型广播标志 \_ 。 由于虚拟设备没有实际的节点号，因此用于虚拟设备的驱动程序没有接收请求的方法，除非它们在广播模式下接收数据包。 如果多个节点分配了相同的地址范围，则只有一个节点会接收到该范围的异步请求。 如果虚拟设备和物理设备的驱动程序分配相同的地址范围，则物理设备的优先级高于虚拟设备，因此物理设备接收数据包。 如果多个虚拟设备分配相同的地址范围，则分配该范围的第一个驱动程序具有优先级。

-   [**请求 \_ \_ \_ 从 \_ 设备对象获取 \_ 地址**](https://msdn.microsoft.com/library/windows/hardware/ff537641)

    虚拟设备没有相应的硬件节点，也没有其自己的节点 ID。 虚拟设备驱动程序在接收到此请求时返回主机控制器的节点 ID，而不是总线上的物理节点的节点 ID。

-   [**请求 \_ 集 \_ 设备 \_ XMIT \_ 属性**](https://msdn.microsoft.com/library/windows/hardware/ff537662)

    虚拟设备不支持此请求，因为没有相应的硬件节点可从中获取节点 ID。

对于所有其他请求，虚拟设备与物理设备之间的行为是相同的。

 

