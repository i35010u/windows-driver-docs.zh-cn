---
title: 中间驱动程序网络数据管理
description: 中间驱动程序网络数据管理
ms.assetid: 12f708b9-32f2-470c-bc4d-7c1b0c1012b1
keywords:
- 中级驱动程序 WDK 网络，网络数据管理
- NDIS 中间驱动程序 WDK，网络数据管理
- 网络数据管理 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e6159b9de085ee2e35304b8a08630b40499804
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844184"
---
# <a name="intermediate-driver-network-data-management"></a>中间驱动程序网络数据管理





中间驱动程序接收[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，其中包含一个或多个关联的 MDLs，从较高级别的驱动程序通过网络发送。 中间驱动程序可以通过调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)来将数据传递到基础驱动程序（如果驱动程序具有无连接的低边缘），或通过调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) （如果驱动程序的底端. 或者，中间驱动程序可以采取一些措施来修改链接缓冲区的内容，或者修改传入数据相对于其他传输的顺序或时间。

根据中间驱动程序的用途，此类驱动程序可以将链接到传入网络\_缓冲区的缓冲区重新打包\_列表结构。 例如，在以下情况下，中间驱动程序将重新打包网络数据：

-   中间驱动程序从过量协议驱动程序接收的数据缓冲区比可通过基础介质在单个缓冲区中发送的数据缓冲区大。 因此，中间驱动程序必须将传入的数据划分为较小的缓冲区。

-   中间驱动程序通过在将每个发送转发到基础驱动程序之前，对数据进行压缩或加密来更改网络数据的长度或内容。

有关创建网络数据管理的信息，请参阅[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)。

NDIS 提供用于克隆和分段[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的接口。 有关克隆和分段结构的详细信息，请参阅[派生的 NET\_BUFFER\_列表结构](derived-net-buffer-list-structures.md)。

NET\_BUFFER\_列表结构可根据需要、驱动程序初始化时间或[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数进行分配。 出于性能原因，中间驱动程序开发人员可以在初始化时分配多个结构，以便[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)已预先分配的资源，以便在其中复制传入数据以指示对于更高级别的驱动程序，并使[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)具有可用的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构（和可能的缓冲区）将传入发送网络数据传递到下一个较低的驱动程序。

如果中间驱动程序将发送数据或接收的数据复制到新的缓冲区或缓冲区，并且最后一个缓冲区中的实际数据长度小于缓冲区的分配长度，则中间驱动程序可以调用**NdisAdjustMdlLength**来调整缓冲区数据的实际长度。

具有无连接下限的中间驱动程序始终从其[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数接收来自基础微型端口适配器的传入数据。

具有面向连接的下边缘的中间驱动程序始终从其[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)函数接收来自基础微型端口适配器的传入数据。

 

 





