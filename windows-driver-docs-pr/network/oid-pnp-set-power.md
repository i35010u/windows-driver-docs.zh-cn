---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.assetid: 21232db2-7484-4878-a2f9-5131c18ecf57
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_SET_POWER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 902d2fd60d315c3430194c7e19f835178b11f330
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567951"
---
# <a name="oidpnpsetpower"></a>OID\_PNP\_SET\_POWER





OID\_PNP\_设置\_POWER OID 通知其基础的网络适配器将转入中指定的设备电源状态的微型端口驱动程序*InformationBuffer*。 设备电源状态指定为以下值之一[ **NDIS\_设备\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/gg602135)值：

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

OID\_PNP\_设置\_电源请求可能会在加[OID\_PNP\_查询\_POWER](oid-pnp-query-power.md)请求。

从 NDIS 6.30 开始，NDIS 将不暂停和重新启动的 NDIS 驱动程序在驱动程序堆栈电源状态转换期间如果满足以下条件：

-   基础的微型端口驱动程序集**NDIS\_微型端口\_特性\_否\_暂停\_ON\_挂起**标志中[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 该驱动程序将指针传递到此结构中对其调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

-   所有基础筛选器驱动程序附加到微型端口驱动程序支持 NDIS 6.30 或更高版本的 NDIS。

-   基础协议的所有驱动程序绑定到微型端口驱动程序支持 NDIS 6.30 或更高版本的 NDIS。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>转换到低功耗状态 (D1 D3)

微型端口驱动程序时处理集请求的 OID\_PNP\_设置\_POWER 转换到低功耗状态，它必须执行以下操作：

-   为所指示的网络设备电源状态完全做好准备的网络适配器。 要实现此目的的微型端口驱动程序执行的任务是依赖于设备的。

-   等待调用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数返回。

-   等待发送请求的网络适配器处理才能完成。 微型端口驱动程序完成后，必须调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数。 该驱动程序应设置**状态**中每个成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构到合适的 NDIS\_状态\_ *Xxx*值。

-   通过调用完成所有挂起的发送请求[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数。 该驱动程序必须设置**状态**中每个成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构**NDIS\_状态\_低\_电源\_状态**。

-   拒绝对所做的所有新发送请求其[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)立即通过调用函数[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数。 该驱动程序必须设置**状态**中每个成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构**NDIS\_状态\_低\_电源\_状态**。

支持 NDIS 6.30 和更高版本的 NDIS 微型端口驱动程序还必须执行以下操作：

-   等待挂起完成接收指示通过调用其[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数。 此外，微型端口驱动程序不得更改[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构或数据的任何正在等待完成的包。

-   处理 OID\_PNP\_设置\_POWER 请求到低功耗状态从已暂停或正在运行的适配器状态。 有关这些状态的详细信息，请参阅[微型端口适配器状态和操作](https://msdn.microsoft.com/library/windows/hardware/ff560490)。

网络适配器将转换为 D3 状态之前，微型端口驱动程序必须先关闭微型端口驱动程序的控制下的所有内容，通过执行以下任务：

-   禁用中断和网络适配器上的 DMA 引擎。

-   停止接收引擎上的网络适配器。

-   不解除分配或修改接收描述符和数据包缓冲区所带来的挂起接收的指示。

-   取消所有 NDIS 计时器。

**请注意**  微型端口驱动程序无法访问的网络适配器后总线驱动程序已转换到 D3 状态的网络适配器。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>转换为全功率状态 (D0)

微型端口驱动程序时处理集请求的 OID\_PNP\_设置\_POWER 转换为全功率状态，它必须将网络适配器的接收引擎还原到相同接收引擎已在之前的状态适配器已转换为低功耗状态。

**请注意**  微型端口驱动程序不能访问或更改任何接收缓冲区所带来的挂起接收的指示。

 

NDIS 调用微型端口驱动程序[ *MiniportRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff559435)后转换到全功率仅状态 NDIS 是否称为驱动程序的正常[ *MiniportPause*](https://msdn.microsoft.com/library/windows/hardware/ff559418)之前向低功耗状态的转换函数。

**请注意**  中间驱动程序必须始终返回**NDIS\_状态\_成功**OID 的查询\_PNP\_设置\_电源。 中间的驱动程序应永远不会传播 OID\_PNP\_设置\_POWER 请求为基础的微型端口驱动程序。

 

## <a name="return-status-codes"></a>返回状态代码


微型端口驱动程序[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数将返回以下值之一用于此请求：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>微型端口驱动程序已成功完成请求。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>微型端口驱动程序将以异步方式完成的请求。 微型端口驱动程序已完成所有处理后，它必须请求成功通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>函数，传递 NDIS_STATUS_SUCCESS<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口驱动程序正在重置。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>NDIS 5.1 和 NDIS 6.0 及更高版本支持。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[*MiniportPause*](https://msdn.microsoft.com/library/windows/hardware/ff559418)

[*MiniportRestart*](https://msdn.microsoft.com/library/windows/hardware/ff559435)

[*MiniportReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559437)

[*MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)

[**NDIS\_DEVICE\_POWER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/gg602135)

[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

 

 




