---
title: 查询和更改 NVGRE 任务卸载状态
description: 本部分介绍如何使用通用路由封装来查询或更改当前的网络虚拟化， (NVGRE) 支持 NVGRE 的微型端口驱动程序的任务卸载状态。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08825ea2d86428e39da4ba8dea5991ce860febcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793397"
---
# <a name="querying-and-changing-nvgre-task-offload-state"></a>查询和更改 NVGRE 任务卸载状态


本部分介绍如何使用通用路由封装来查询或更改当前的 [网络虚拟化， (NVGRE) ](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md) 支持 NVGRE 的微型端口驱动程序的任务卸载状态。 默认情况下，可以启用 NVGRE 任务卸载，但它在默认情况下不能处于活动状态。 在使用 NDIS 协议或筛选器驱动程序显式启用此功能之前，NIC 不应在封装的数据包上开始执行任务卸载。

## <a name="querying-nvgre-task-offload-state"></a>查询 NVGRE 任务卸载状态


若要查询微型端口驱动程序的当前 NVGRE 任务卸载状态，NDIS 协议或筛选器驱动程序使用 [OID \_ TCP \_ 卸载 \_ 当前的 \_ 配置](./oid-tcp-offload-current-config.md) OID 请求。 这会返回 [**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle) 结构，其 **EncapsulatedPacketTaskOffloadGre** 成员是一个 [**ndis \_ 封装的 \_ 数据包 \_ 任务 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload) 结构，其中包含 **\_ \_ 支持的 ndis 卸载** （如果当前已为 GRE 封装的数据包启用了这些卸载，否则 **\_ \_ 不 \_ 支持 ndis 卸载** ）。 NDIS 处理此 OID，但不将其向下传递到小型端口。

**注意**  若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，请使用 [oid \_ TCP \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md) Oid 请求，如 [确定网络适配器的 NVGRE 任务卸载功能](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)中所述。

 

## <a name="changing-nvgre-task-offload-state"></a>更改 NVGRE 任务卸载状态


NDIS 协议或筛选器驱动程序可以通过发出 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求来启用或禁用 NVGRE 任务卸载。 此 OID 使用 [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构。 在此结构中， **EncapsulatedPacketTaskOffload** 成员可以具有以下值：

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

 

当微型端口驱动程序处理 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求后，它必须发出 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 和 "更新的卸载" 状态。

当微型端口驱动程序接收到指定了 **NDIS \_ 卸载 \_ 设置为 \_ OFF** 标志的 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md)OID 请求时，驱动程序应指示在完成 OID 请求之前，已部分处理的任何现有的已封装包，以使任务在堆栈中上移。

常规数据包的基本任务卸载由现有 Oid （如 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) 和 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md)）启用。 **EncapsulatedPacketTaskOffload** 成员设置补充了这些 oid，并指示 NIC 还对封装的数据包执行了这些卸载。

 

