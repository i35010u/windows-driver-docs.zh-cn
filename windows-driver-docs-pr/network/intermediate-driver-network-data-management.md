---
title: 中间驱动程序网络数据管理
description: 中间驱动程序网络数据管理
ms.assetid: 12f708b9-32f2-470c-bc4d-7c1b0c1012b1
keywords:
- 中间驱动程序 WDK 网络、 网络数据管理
- NDIS 中间层驱动程序 WDK、 网络数据管理
- 网络数据管理 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbe36a437adb9db84fcc7dff9656baef6aa2113c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391661"
---
# <a name="intermediate-driver-network-data-management"></a>中间驱动程序网络数据管理





中间的驱动程序将收到[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)具有一个或多个结构关联 MDLs 从更高级别的驱动程序，即可通过网络发送。 中间驱动程序可以通过数据通过传递到基础驱动程序调用[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)驱动程序有无连接的下边缘，或通过调用[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)如果驱动程序有面向连接的下边缘。 或者，中间驱动程序可以执行某些操作来修改链接的缓冲区排序或计时相对于其他传输的传入数据的内容。

具体取决于中间驱动程序的目的，此类驱动程序可以重新打包链接到传入 NET 的缓冲区\_缓冲区\_列表结构。 例如，中间驱动程序重新打包在以下情况下的网络数据：

-   中间驱动程序将收到较大数据的缓冲区从基础的协议驱动程序不是可以通过基础媒体发送单个缓冲区中。 因此，中间驱动程序必须将传入的数据划分为较小的缓冲区。

-   中间驱动程序更改的长度或网络压缩或加密之前每个转发数据的数据将发送到基础驱动程序的内容。

有关创建网络数据管理的信息，请参阅[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)。

NDIS 克隆和片段提供了接口[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 有关克隆和来分段结构的详细信息，请参阅[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)。

NET\_缓冲区\_可以根据需要在驱动程序初始化时，或在已分配列表结构[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。 中间驱动程序开发人员可以如有必要，出于性能原因，分配的结构数在初始化时，以便[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)具有预先分配向其复制到更高级别的驱动程序，该值指示传入的数据的资源，使[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)可用[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构 （和可能的缓冲区） 将传入网络将数据发送到下一个较低的驱动程序。

如果中间驱动程序将数据发送或接收的数据复制到新的缓冲区或缓冲区，并且最后一个缓冲区中的实际数据的长度小于分配的缓冲区的长度，中间驱动程序可以调用**NdisAdjustMdlLength**调整到的数据的实际长度的缓冲区。

使用无连接的下边缘中间驱动程序始终接收传入的数据从基础的微型端口适配器从其[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)函数。

使用面向连接的下边缘中间驱动程序始终接收传入的数据从基础的微型端口适配器从其[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)函数。

 

 





