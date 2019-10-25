---
title: 取消发送操作
description: 取消发送操作
ms.assetid: 5bd7a815-4e4d-4259-b322-f4f8d07f2e1a
keywords:
- 网络数据 WDK，发送
- 数据 WDK 网络，发送
- 包 WDK 网络，发送
- 发送数据 WDK 网络
- NDIS_SET_NET_BUFFER_LIST_CANCEL_ID
- 取消发送操作 WDK 网络
- 取消 Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a90fbd3b032a8372f1ec8a8e285fc971f45d3ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838212"
---
# <a name="canceling-a-send-operation"></a>取消发送操作





下图说明了如何取消发送操作。

![阐释取消发送操作的关系图](images/netbuffercancelsend.png)

驱动程序将调用[**NDIS\_设置\_net\_buffer\_列表\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-set-net-buffer-list-cancel-id)对于每个要传递给较低级别驱动程序以进行传输的[**网络\_缓存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)\_ NDIS\_设置\_NET\_BUFFER\_列表\_CANCEL\_ID 函数使用取消标识符标记指定的数据包。

在将取消 Id 分配给数据包之前，驱动程序应调用[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)以获取它分配的每个取消 ID 的高序位字节。 这可确保驱动程序不会复制由系统中的其他驱动程序分配的取消 Id。 通常，驱动程序从**DriverEntry**例程调用**NdisGeneratePartialCancelId**一次;但是，驱动程序可以多次调用**NdisGeneratePartialCancelId**来获取多个部分取消标识符。

若要取消已标记的 NET\_BUFFER\_列表结构中的数据的挂起传输，驱动程序将取消 ID 传递到[**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)函数。 驱动程序可以通过调用[**NDIS\_\_获取**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)\_缓冲区\_列表结构的取消 ID，\_\_取消\_ID 宏。

如果驱动程序使用相同的取消标识符来标记所有[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，则它可以通过对**NdisCancelSendNetBufferLists**的单个调用来取消所有挂起的传输。 如果驱动程序将 NET\_\_BUFFER 的子组中的所有网络\_缓冲区\_列表结构标记为具有唯一标识符的列表结构，则它可以通过单一调用**NdisCancelSendNetBufferLists**。

NDIS 调用绑定上适当的低级驱动程序的[*MiniportCancelSend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)函数。 中止挂起的传输后，基础微型端口驱动程序将调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数，以返回 NET\_缓冲区\_列表结构和 NDIS\_状态的完成状态\_已中止发送\_。 反过来，NDIS 调用适当的驱动程序的[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数。

在其*ProtocolSendNetBufferListsComplete*函数中，协议驱动程序可以调用 NDIS\_设置\_NET\_BUFFER\_列表\_取消\_ID，并将*CancelId*设置为**NULL**。 这会阻止 NET\_缓冲器\_列表不小心被使用过时的取消 ID 再次使用。

 

 





