---
title: 查询和更改 NVGRE 任务卸载状态
description: 本部分介绍如何使用支持 NVGRE 的微型端口驱动程序的通用路由封装（NVGRE）任务卸载状态来查询或更改当前的网络虚拟化。
ms.assetid: 2F493F35-0D6D-4D23-A5CD-FA3990B3EAB5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bee8995ef4bd7e3856efc2ff41103e31d7d79910
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844900"
---
# <a name="querying-and-changing-nvgre-task-offload-state"></a>查询和更改 NVGRE 任务卸载状态


本部分介绍如何使用支持 NVGRE 的微型端口驱动程序的[通用路由封装（NVGRE）任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)状态来查询或更改当前的网络虚拟化。 默认情况下，可以启用 NVGRE 任务卸载，但它在默认情况下不能处于活动状态。 在使用 NDIS 协议或筛选器驱动程序显式启用此功能之前，NIC 不应在封装的数据包上开始执行任务卸载。

## <a name="querying-nvgre-task-offload-state"></a>查询 NVGRE 任务卸载状态


为了查询微型端口驱动程序的当前 NVGRE 任务卸载状态，NDIS 协议或筛选器驱动程序使用[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) OID 请求。 这会返回[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle)结构，该结构的**ENCAPSULATEDPACKETTASKOFFLOADGRE**成员是[**封装\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构中的 ndis\_，它包含在当前为 GRE 封装的数据包启用了这些卸载，并且**未\_支持**的情况下支持的**ndis\_** 卸载\_\_\_ NDIS 处理此 OID，但不将其向下传递到小型端口。

**请注意**  若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，请使用[oid\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 请求，如[确定网络适配器的 NVGRE 任务卸载功能](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)中所述。

 

## <a name="changing-nvgre-task-offload-state"></a>更改 NVGRE 任务卸载状态


NDIS 协议或筛选器驱动程序可以通过[\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，来启用或禁用 NVGRE 任务卸载。 此 OID 使用[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构。 在此结构中， **EncapsulatedPacketTaskOffload**成员可以具有以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong></p></td>
<td align="left"><p>NVGRE 任务卸载状态保持不变。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_ON</strong></p></td>
<td align="left"><p>指定此标志可启用 NVGRE 任务卸载。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NDIS_OFFLOAD_SET_OFF</strong></p></td>
<td align="left"><p>指定此标志可禁用 NVGRE 任务卸载。</p></td>
</tr>
</tbody>
</table>

 

当微型端口驱动程序处理[oid\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求后，它必须使用更新的卸载状态\_当前\_的配置状态指示发出[**NDIS\_状态\_的任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)。

当微型端口驱动程序接收到[oid\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求（其中，已指定**NDIS\_卸载\_设置\_OFF**标志），驱动程序应指示在完成 OID 请求之前部分处理的任何现有封装的数据包，以使任务在堆栈中上移。

常规数据包的基本任务卸载由现有 Oid （如 Oid）启用， [\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)和[oid\_接收\_FILTER\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)。 **EncapsulatedPacketTaskOffload**成员设置补充了这些 oid，并指示 NIC 还对封装的数据包执行了这些卸载。

 

 





