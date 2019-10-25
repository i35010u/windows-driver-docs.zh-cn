---
title: 取消筛选器驱动程序中的发送请求
description: 取消筛选器驱动程序中的发送请求
ms.assetid: afa9c8d3-b30b-4009-8428-d31719885154
keywords:
- 取消发送操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56476fcc95135bddfbe23ec4e9476e53efa69201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835280"
---
# <a name="canceling-a-send-request-in-a-filter-driver"></a>取消筛选器驱动程序中的发送请求





筛选器驱动程序可以取消由筛选器驱动程序或由过量驱动程序生成的发送请求。

### <a name="canceling-filter-driver-send-requests"></a>正在取消筛选器驱动程序发送请求

下图说明了如何取消由筛选器驱动程序生成的发送请求。

![说明取消由筛选器驱动程序发起的发送请求的关系图](images/filtercancelsend.png)

筛选器驱动程序将调用[**NDIS\_设置\_net\_buffer\_列表\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-set-net-buffer-list-cancel-id)为发送操作创建的每个[**net\_缓存\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的取消\_ID 宏。 NDIS\_设置\_NET\_BUFFER\_列表\_CANCEL\_ID 函数使用取消标识符标记指定数据。

在为网络数据分配取消 Id 之前，筛选器驱动程序必须调用[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)以获取它分配的每个取消 ID 的高序位字节。 这可确保驱动程序不会复制由系统中的其他驱动程序分配的取消 Id。 驱动程序通常从[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用**NdisGeneratePartialCancelId**一次。 但是，驱动程序可以多次调用**NdisGeneratePartialCancelId**来获取多个部分取消标识符。

若要在标记的网络\_缓冲区\_列表结构中取消挂起的数据传输，筛选器驱动程序会将取消 ID 传递到[**NdisFCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists)函数。 驱动程序可以通过调用[**NDIS\_\_获取**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)\_缓冲区\_列表结构的取消 ID，\_\_取消\_ID 宏。

如果筛选器驱动程序使用相同的取消标识符来标记所有网络\_缓冲区\_列表结构，则它可以通过对**NdisFCancelSendNetBufferLists**的单个调用取消所有挂起的传输。 如果筛选器驱动程序将 NET\_\_BUFFER 的子组中的所有 NET\_缓冲区\_列表结构标记为具有唯一标识符的列表结构，则它可以通过调用**NdisFCancelSendNetBufferLists**。

NDIS 调用底层驱动程序的取消发送功能。 中止挂起的传输后，基础驱动程序将调用发送完成函数（例如[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)），以返回具有 NDIS 完成状态的 NET\_缓冲区\_列表结构\_已中止发送\_\_状态。 反过来，NDIS 调用筛选器驱动程序的[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)函数。

在*FilterSendNetBufferListsComplete*中，筛选器驱动程序可以调用 NDIS\_设置\_NET\_BUFFER\_列表\_取消\_ID，并将*CancelId*设置为**NULL**。 这会阻止 NET\_缓冲区\_列表意外地使用过时的取消 ID 再次使用。

### <a name="canceling-send-requests-originated-by-overlying-drivers"></a>正在取消过量驱动程序发出的发送请求

下图说明了如何取消由过量驱动程序生成的发送请求。

![说明取消由过量驱动程序发起的发送请求的关系图](images/cancelfiltersend.png)

过量驱动程序调用取消发送函数（ [**NdisFCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists)或[**NdisCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscancelsendnetbufferlists)）以取消未完成的发送请求。 在发出发送请求之前，这些过量驱动程序必须使用取消 ID 标记发送数据。

NDIS 调用筛选器驱动程序的[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)函数来取消使用指定的取消标识符标记的所有[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的传输。

*FilterCancelSendNetBufferLists*执行以下操作：

1.  遍历指定筛选器模块的筛选器驱动程序驱动程序驱动程序的排队网络\_缓冲区\_列表结构的列表，并调用[**NDIS\_获取\_NET\_BUFFER\_list\_CANCEL\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-get-net-buffer-list-cancel-id)宏获取每个结构的取消标识符。 筛选器驱动程序会比较 NDIS\_获取\_NET\_缓冲区\_列表\_CANCEL\_ID 返回的取消 id，并将 NDIS 传递到*FilterCancelSendNetBufferLists*。

2.  从发送队列中删除所有 NET\_缓冲区\_列表结构，其取消标识符与指定的取消标识符相匹配。

3.  调用[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数，使所有未链接的 NET\_缓冲区\_列表结构返回结构。 筛选器驱动程序将 NET\_缓冲区\_列表结构的 "状态" 字段设置为 "NDIS\_状态\_" 发送\_已中止 "。

4.  调用**NdisFCancelSendNetBufferLists**函数以将取消发送请求传递到底层驱动程序。 筛选器驱动程序将传递从过量驱动程序收到的取消标识符。 取消操作将按筛选器驱动程序发起的取消发送操作那样继续。

 

 





