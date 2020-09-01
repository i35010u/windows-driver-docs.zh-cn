---
title: NDIS_STATUS_RECEIVE_QUEUE_STATE
description: NDIS_STATUS_RECEIVE_QUEUE_STATE 状态向过量驱动程序指出虚拟机队列 (VMQ) 接收队列的队列状态已更改。
ms.assetid: 59b42de9-6aa5-445e-a39a-de2421c945ea
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RECEIVE_QUEUE_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cce0fd621277a535cadb31187fe44a15fa9a7c2b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206077"
---
# <a name="ndis_status_receive_queue_state"></a>NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态


"NDIS \_ 状态 \_ 接收 \_ 队列 \_ 状态" 状态向过量驱动程序指示虚拟机队列 (VMQ) 接收队列的队列状态已更改。

<a name="remarks"></a>备注
-------

支持虚拟机队列接口的 NDIS 6.20 和更高的微型端口驱动程序会生成此状态指示。

微型端口驱动程序在[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员中提供[**ndis \_ 接收 \_ 队列 \_ 状态**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构。

更改为 *DMA 停止* 状态是唯一需要的队列状态更改指示。 微型端口驱动程序必须在收到 [OID \_ 接收 \_ 筛选器 \_ 释放 \_ 队列](./oid-receive-filter-free-queue.md) 集请求并停止 DMA 之后指示此状态。 在这种情况下，微型端口驱动程序将[**NDIS \_ 接收 \_ 队列 \_ 状态**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)结构的**QueueState**成员设置为**NdisReceiveQueueOperationalStateDmaStopped**。

当微型端口驱动程序收到 [OID \_ 接收 \_ 筛选器 \_ 释放 \_ 队列](./oid-receive-filter-free-queue.md) 集请求后，必须将 DMA 停止到为指定队列分配的任何共享内存。

如果微型端口驱动程序由于某些其他原因而停止了 DMA (例如，它释放了队列) 上的最后一个筛选器，则队列不应进入 *DMA 停止* 状态。 但是，如果队列中没有设置任何筛选器，则可以在 "已 *暂停* " 或 " *正在运行* " 状态下停止 DMA。

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


[**NDIS \_ 接收 \_ 队列 \_ 状态**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_queue_state)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ 接收 \_ 筛选器 \_ 可用 \_ 队列](./oid-receive-filter-free-queue.md)

 

