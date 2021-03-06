---
title: 取消筛选器驱动程序中的发送请求
description: 取消筛选器驱动程序中的发送请求
keywords:
- 取消发送操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c268686f85c618d278cc9ad100370decfb6270ad
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248180"
---
# <a name="canceling-a-send-request-in-a-filter-driver"></a>取消筛选器驱动程序中的发送请求





筛选器驱动程序可以取消由筛选器驱动程序或由过量驱动程序生成的发送请求。

### <a name="canceling-filter-driver-send-requests"></a>正在取消筛选器驱动程序发送请求

下图说明了如何取消由筛选器驱动程序生成的发送请求。

![说明取消由筛选器驱动程序发起的发送请求的关系图](images/filtercancelsend.png)

筛选器驱动程序为为发送操作创建的每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构调用 [**NDIS \_ 设置 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_set_net_buffer_list_cancel_id)宏。 NDIS \_ 设置 \_ NET \_ BUFFER \_ LIST \_ CANCEL \_ ID 函数使用取消标识符标记指定数据。

在为网络数据分配取消 Id 之前，筛选器驱动程序必须调用 [**NdisGeneratePartialCancelId**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid) 以获取它分配的每个取消 ID 的高序位字节。 这可确保驱动程序不会复制由系统中的其他驱动程序分配的取消 Id。 驱动程序通常从 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用 **NdisGeneratePartialCancelId** 一次。 但是，驱动程序可以多次调用 **NdisGeneratePartialCancelId** 来获取多个部分取消标识符。

若要取消已标记的网络缓冲区列表结构中等待传输的数据 \_ \_ ，筛选器驱动程序将取消 ID 传递到 [**NdisFCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists) 函数。 驱动程序可以 \_ \_ 通过调用 [**NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_get_net_buffer_list_cancel_id) 宏获取网络缓冲区列表结构的取消 id。

如果筛选器驱动程序 \_ \_ 使用相同的取消标识符来标记所有网络缓冲区列表结构，则它可以通过对 **NdisFCancelSendNetBufferLists** 的单个调用来取消所有挂起的传输。 如果筛选器驱动程序将 \_ \_ 网络缓冲区列表结构的子组内的所有网络缓冲区列表结构标记为 \_ \_ 唯一标识符，则可以通过一次调用 **NdisFCancelSendNetBufferLists** 取消该子组内的所有挂起传输。

NDIS 调用底层驱动程序的取消发送功能。 中止挂起的传输后，基础驱动程序将调用发送完成函数 (例如 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)) ，以返回已 \_ \_ 完成状态为 NDIS \_ 状态 \_ send 中止的网络缓冲区列表结构 \_ 。 反过来，NDIS 调用筛选器驱动程序的 [*FilterSendNetBufferListsComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete) 函数。

在 *FilterSendNetBufferListsComplete* 中，筛选器驱动程序可以调用 NDIS \_ 设置 \_ 网络 \_ 缓冲区 \_ 列表 \_ CANCEL \_ ID，并将 *CancelId* 设置为 **NULL**。 这会阻止 NET \_ BUFFER \_ 列表意外地使用过时的取消 ID 再次使用。

### <a name="canceling-send-requests-originated-by-overlying-drivers"></a>正在取消过量驱动程序发出的发送请求

下图说明了如何取消由过量驱动程序生成的发送请求。

![说明取消由过量驱动程序发起的发送请求的关系图](images/cancelfiltersend.png)

过量驱动程序调用取消发送函数 ( [**NdisFCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists) 或 [**NdisCancelSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)) 取消未完成的发送请求。 在发出发送请求之前，这些过量驱动程序必须使用取消 ID 标记发送数据。

NDIS 调用筛选器驱动程序的 [*FilterCancelSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists) 函数来取消使用指定的取消标识符标记的所有 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的传输。

*FilterCancelSendNetBufferLists* 执行以下操作：

1.  遍历指定筛选器模块的已排队网络缓冲区列表结构的筛选器驱动程序列表 \_ \_ ，并调用 [**NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_get_net_buffer_list_cancel_id) 宏，以获取每个结构的取消标识符。 筛选器驱动程序将 NDIS \_ 获取 \_ 网络 \_ 缓冲区 \_ 列表 \_ 取消 id 返回的取消 Id \_ 与 NDIS 传递给 *FilterCancelSendNetBufferLists* 的取消 id 进行比较。

2.  从发送队列中删除 (取消) 所有网络 \_ 缓冲区 \_ 列表结构的取消，这些结构的取消标识符与指定的取消标识符相匹配。

3.  为所有[](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)未链接的网络 \_ 缓冲区列表结构调用 NdisFSendNetBufferListsComplete 函数 \_ 以返回结构。 筛选器驱动程序将网络缓冲区列表结构的 "状态" 字段设置 \_ \_ 为 "NDIS \_ 状态发送已中止" \_ \_ 。

4.  调用 **NdisFCancelSendNetBufferLists** 函数以将取消发送请求传递到底层驱动程序。 筛选器驱动程序将传递从过量驱动程序收到的取消标识符。 取消操作将按筛选器驱动程序发起的取消发送操作那样继续。

 

