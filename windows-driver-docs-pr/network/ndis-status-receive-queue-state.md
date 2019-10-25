---
title: NDIS_STATUS_RECEIVE_QUEUE_STATE
description: NDIS_STATUS_RECEIVE_QUEUE_STATE 状态向过量驱动程序指示虚拟机队列（VMQ）接收队列的队列状态已更改。
ms.assetid: 59b42de9-6aa5-445e-a39a-de2421c945ea
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RECEIVE_QUEUE_STATE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b85176044df4fe91fdb37ec2b3aa6fac73f8608d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843520"
---
# <a name="ndis_status_receive_queue_state"></a>NDIS\_状态\_接收\_队列\_状态


\_接收\_队列\_状态状态的 NDIS\_状态向过量驱动程序指示虚拟机队列（VMQ）接收队列的队列状态已更改。

<a name="remarks"></a>备注
-------

支持虚拟机队列接口的 NDIS 6.20 和更高的微型端口驱动程序会生成此状态指示。

微型端口驱动程序提供[**ndis\_接收\_队列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)，在[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员中\_状态结构。

更改为*DMA 停止*状态是唯一需要的队列状态更改指示。 微型端口驱动程序必须在收到 OID 之后指示此状态[\_接收\_FILTER\_可用\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集请求并停止 DMA。 在这种情况下，微型端口驱动程序[**会将 NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构的**QueueState**成员设置为**NdisReceiveQueueOperationalStateDmaStopped**。

在微型端口驱动程序收到[OID\_接收\_FILTER\_FREE\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集请求后，它必须停止为指定队列分配的任何共享内存的 DMA。

如果微型端口驱动程序由于某种其他原因（例如，释放了队列上的最后一个筛选器）而停止了 DMA，则队列不应进入*Dma 停止*状态。 但是，如果队列中没有设置任何筛选器，则可以在 "已*暂停*" 或 "*正在运行*" 状态下停止 DMA。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_接收\_筛选器\_可用\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

 

 




