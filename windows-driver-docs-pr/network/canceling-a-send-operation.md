---
title: 取消发送操作
description: 取消发送操作
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
ms.openlocfilehash: d7fb2aa950964958e321cfb71ea81a7e904cd210
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839895"
---
# <a name="canceling-a-send-operation"></a>取消发送操作





下图说明了如何取消发送操作。

![阐释取消发送操作的关系图](images/netbuffercancelsend.png)

驱动程序为传递给较低级别驱动程序以进行传输的每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构调用 [**NDIS \_ 设置 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_set_net_buffer_list_cancel_id)宏。 NDIS \_ 设置 \_ NET \_ BUFFER \_ LIST \_ CANCEL \_ ID 函数使用取消标识符标记指定的数据包。

在将取消 Id 分配给数据包之前，驱动程序应调用 [**NdisGeneratePartialCancelId**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid) 以获取它分配的每个取消 ID 的高序位字节。 这可确保驱动程序不会复制由系统中的其他驱动程序分配的取消 Id。 通常，驱动程序从 **DriverEntry** 例程调用 **NdisGeneratePartialCancelId** 一次;但是，驱动程序可以多次调用 **NdisGeneratePartialCancelId** 来获取多个部分取消标识符。

若要在标记的网络缓冲区列表结构中取消挂起的数据传输 \_ \_ ，驱动程序将取消 ID 传递到 [**NdisCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists) 函数。 驱动程序可以 \_ \_ 通过调用 [**NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_get_net_buffer_list_cancel_id) 宏获取网络缓冲区列表结构的取消 id。

如果驱动程序使用相同的取消标识符来标记所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，则它可以通过一次调用 **NdisCancelSendNetBufferLists** 取消所有挂起的传输。 如果驱动程序 \_ \_ 使用唯一标识符标记网络缓冲区列表结构子组内的所有网络缓冲区列表结构 \_ \_ ，则可以通过对 **NdisCancelSendNetBufferLists** 的单个调用来取消该子组内的所有挂起的传输。

NDIS 调用绑定上适当的低级驱动程序的 [*MiniportCancelSend*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send) 函数。 中止挂起的传输后，基础微型端口驱动程序将调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数，以返回网络 \_ 缓冲区 \_ 列表结构，并中止 NDIS 状态发送的完成状态 \_ \_ \_ 。 反过来，NDIS 调用适当的驱动程序的 [**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete) 函数。

在其 *ProtocolSendNetBufferListsComplete* 函数中，协议驱动程序可以调用 NDIS \_ 设置 \_ 网络 \_ 缓冲区 \_ 列表 \_ CANCEL ID， \_ 并将 *CancelId* 设置为 **NULL**。 这会阻止网络 \_ 缓冲区 \_ 列表意外地与过时的取消 ID 再次使用。

 

