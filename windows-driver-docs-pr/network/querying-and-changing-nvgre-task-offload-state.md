---
title: 查询和更改 NVGRE 任务卸载状态
description: 本部分介绍如何查询或更改当前网络虚拟化使用 NVGRE 支持的微型端口驱动程序的通用路由封装 (NVGRE) 任务卸载状态。
ms.assetid: 2F493F35-0D6D-4D23-A5CD-FA3990B3EAB5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61d149da086570c01036e74de20ddf7296fc9d87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563438"
---
# <a name="querying-and-changing-nvgre-task-offload-state"></a>查询和更改 NVGRE 任务卸载状态


本部分介绍如何查询或更改当前[网络虚拟化使用通用路由封装 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)NVGRE 支持的微型端口驱动程序的状态。 默认情况下，可以启用 NVGRE 任务卸载，但不是能在操作上处于活动状态，默认值。 NIC 应开始直到 NDIS 协议或筛选器驱动程序中显式启用此功能对封装的数据包执行任务卸载。

## <a name="querying-nvgre-task-offload-state"></a>查询 NVGRE 任务卸载状态


若要查询的微型端口驱动程序的当前 NVGRE 任务卸载状态，NDIS 协议或筛选器驱动程序将使用[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID 请求。 这将返回[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566705)结构，其**EncapsulatedPacketTaskOffloadGre**成员是[ **NDIS\_封装\_数据包\_任务\_卸载**](https://msdn.microsoft.com/library/windows/hardware/jj991956)结构，其中包含**NDIS\_卸载\_支持**如果这些卸载当前启用了 GRE 封装的数据包，并**NDIS\_卸载\_不\_支持**否则为。 NDIS 处理此 OID 并不将它传递到微型端口。

**请注意**  若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，请使用[OID\_TCP\_卸载\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569806)OID请求中所述[确定 NVGRE 任务卸载功能的网络适配器的](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)。

 

## <a name="changing-nvgre-task-offload-state"></a>更改 NVGRE 任务卸载状态


NDIS 协议或筛选器驱动程序可以启用或禁用通过发出 NVGRE 任务卸载[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求。 使用此 OID [ **NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)结构。 在此结构中， **EncapsulatedPacketTaskOffload**成员可以具有以下值：

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
<td align="left"><p>指定此标志，以禁用 NVGRE 任务卸载。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序进程后[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求时，必须颁发[ **NDIS\_状态\_任务\_卸载\_当前\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)使用更新的状态指示卸载状态。

当微型端口驱动程序收到[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求在其中**NDIS\_卸载\_设置\_关闭**指定标志，该驱动程序应指示与任何现有封装对任务完成 OID 请求之前卸载在堆栈中向上部分处理的数据包。

基本任务将卸载通过现有 Oid 如启用正常数据包[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)并[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)。 **EncapsulatedPacketTaskOffload**成员设置是这些 Oid 的补充，指示要还执行这些卸载对于封装的数据包的 NIC。

 

 





