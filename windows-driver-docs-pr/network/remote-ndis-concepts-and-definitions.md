---
title: 远程 NDIS 概念和定义
description: 远程 NDIS 概念和定义
ms.assetid: caf01e69-9368-4b9b-a343-ef17a2154bb8
keywords:
- 远程 NDIS WDK 网络、 概念
- 远程 NDIS WDK 网络定义
- 远程 NDIS WDK 网络、 控制通道
- 远程 NDIS WDK 网络、 数据通道
- 远程 NDIS WDK 网络、 停止
- 控制通道 WDK 网络
- 控制通道 WDK 网络、 初始化
- 控制通道 WDK 网络、 清除
- 数据通道 WDK 网络
- 数据通道 WDK 网络、 初始化
- 数据通道 WDK 网络、 清除
- 远程 NDIS WDK 网络、 设备状态
- 设备状态 WDK 网络
- 远程 NDIS WDK 网络、 流控制
- 远程 NDIS WDK 网络、 重置通信通道
- 通信通道 WDK 网络
- 远程 NDIS WDK 网络、 消息封装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10377ce25890a86721f9f3e52e8af631c991c8a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547445"
---
# <a name="remote-ndis-concepts-and-definitions"></a>远程 NDIS 概念和定义





本部分中概述的通信通道和用于在主机和远程 NDIS 设备之间进行通信的较低层驱动程序上的远程 NDIS 要求。 在本部分中的设备状态转换以及初始化、 停止和重置等的主要操作还介绍了。

-   **控制通道**

    控制通道必须可靠，并确保按顺序的传递。 它用于除网络数据包的传输的所有通信。 所有必需的控制消息，除非[远程\_NDIS\_暂停\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570613)并[远程\_NDIS\_指示\_状态\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570617)，是由主机启动的请求和响应交换。 设备必须在每个总线指定的超时期限内做出响应。

-   **数据通道**

    数据通道专门用于网络数据包的传输。 它可能包含多个 subchannels （例如，对于不同的服务质量） 为相应的总线定义的一样。

-   **初始化和拆卸**

    控制和数据通道初始化并设置指定为相应的总线。 主机发送[远程\_NDIS\_初始化\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570624)到远程 NDIS 设备的消息。 远程 NDIS 设备提供支持 （无连接或面向连接的），其类型有关的信息中和响应消息中的版本[远程\_NDIS\_初始化\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570621).

    在主机或远程 NDIS 设备可以消除通过通信通道[远程\_NDIS\_暂停\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570613)消息。 在收到此消息将丢弃所有未完成的请求和数据包。

-   **设备状态定义**

    以下 bus 级别初始化设备被认为处于 RNDIS 未初始化状态。 在接收时[远程\_NDIS\_初始化\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570624) ，并且通过远程\_NDIS\_初始化\_CMPLT RNDIS状态\_状态\_成功，则设备将进入 RNDIS 初始化状态。

    一旦收到远程\_NDIS\_设置\_MSG OID 的指定非零值的筛选器值\_常规\_当前\_数据包\_筛选器，则设备将进入RNDIS 数据初始化状态。

    在状态 RNDIS 数据的初始化，接收的远程\_NDIS\_设置\_指定为 0 的消息筛选器值为 OID\_常规\_当前\_数据包\_筛选器强制设备回 RNDIS 初始化状态。

    接收的远程\_NDIS\_暂停\_MSG 或断开连接或硬重置在任何时间强制为 RNDIS 未初始化状态的设备的总线的级别。

-   **Halt**

    在任何设备处于 RNDIS 初始化或 RNDIS 数据初始化状态的时间，在主计算机可能会终止该设备的远程 NDIS 功能通过发送远程\_NDIS\_暂停\_到设备的消息。

-   **正在重置通信通道**

    出现错误，例如消息超时发生时，会重置通信通道。 主机可能发起在设备处于 RNDIS 初始化状态时发送消息的任何时间重置[远程\_NDIS\_重置\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570648)设备和设备必须发送响应完成重置时的消息。 例如，主机可能会出现错误，例如消息超时发生时启动重置。

    请注意，这是软重置意义上说，任何句柄 (例如，对于面向连接的设备的 VCs) 仍然有效后重置。 远程 NDIS 设备重置过程的一部分将放弃所有未完成的请求和数据包。 远程设备可能会重置某些硬件组件，但保持通信通道的更新保持不变。

    如果远程 NDIS 设备执行重新启动，则此事件是相当于"删除"跟"添加"插事件。 将暂停主机 NDIS 微型端口驱动程序，并将其删除，并将添加一个新实例，并将其启动。 所有 bus 级别和远程 NDIS 初始化都将重新执行。 远程 NDIS 设备可能会自行重新启动关键设备故障。

-   **流控制**

    远程 NDIS 设备可能需要进行数据流控制以防止溢出数据包使用其数据缓冲区中的主机。 任何流控制预配或要求特定的总线。

-   **数值字节排序**

    远程 NDIS 消息中的所有数值必须在 little-endian 格式进行都编码 (最低有效字节第一个)。

-   **NDIS 消息封装**

    NDIS 消息封装在本机总线的消息或基元的方式没有远程 NDIS 规范。

 

 





