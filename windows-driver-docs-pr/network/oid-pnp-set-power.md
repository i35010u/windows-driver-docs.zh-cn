---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.assetid: 21232db2-7484-4878-a2f9-5131c18ecf57
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_SET_POWER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 67bfd40a8c88918d5fe2c29a84b657dfc03f8ee0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844036"
---
# <a name="oid_pnp_set_power"></a>OID\_PNP\_集\_电源





OID\_PNP\_集\_电源 OID 通知小型端口驱动程序，其基础网络适配器将转换为*InformationBuffer*中指定的设备电源状态。 设备电源状态指定为下列[**NDIS\_设备之一\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)值：

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

OID\_PNP\_集\_POWER request 前面可能有[oid\_PNP\_查询\_POWER](oid-pnp-query-power.md) request。

从 NDIS 6.30 开始，如果满足以下条件，NDIS 将不会在驱动程序堆栈中暂停和重新启动 NDIS 驱动程序：

-   基础微型端口驱动程序将 ndis **\_微型端口设置为\_属性\_不\_暂停\_** [**ndis\_端口\_适配器\_注册\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)\_ 驱动程序在其对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的调用中传递指向此结构的指针。

-   附加到微型端口驱动程序的所有过量筛选器驱动程序都支持 NDIS 6.30 或更高版本的 NDIS。

-   绑定到微型端口驱动程序的所有过量协议驱动程序都支持 NDIS 6.30 或更高版本的 NDIS。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>过渡到低功耗状态（D1-D3）

当微型端口驱动程序处理\_PNP\_\_设置的 OID 的设置请求时，必须执行以下操作：

-   为指示的网络设备电源状态充分准备网络适配器。 微型端口驱动程序执行的任务是与设备相关的。

-   等待对[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数的调用返回。

-   等待网络适配器处理的发送请求完成。 完成后，微型端口驱动程序必须调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数。 驱动程序应将每个[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的**状态**成员设置为相应的 NDIS\_状态\_*Xxx*值。

-   通过调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数完成所有挂起的发送请求。 驱动程序必须将每个[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的**状态**成员设置\_列表结构到**NDIS\_状态\_低\_POWER\_状态**。

-   通过调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数，立即拒绝对其[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数发出的所有新发送请求。 驱动程序必须将每个[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的**状态**成员设置\_列表结构到**NDIS\_状态\_低\_POWER\_状态**。

支持 NDIS 6.30 和更高版本的 NDIS 的微型端口驱动程序还必须执行以下操作：

-   不等待通过调用[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数来完成挂起的接收指示。 此外，微型端口驱动程序不得为等待完成的任何数据包更改[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构或数据。

-   处理 OID\_PNP\_从已暂停或正在运行的适配器状态\_电源请求设置为低功耗状态。 有关这些状态的详细信息，请参阅[微型端口适配器状态和操作](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-adapter-states-and-operations)。

在网络适配器转换到 D3 状态之前，微型端口驱动程序必须通过执行以下任务来关闭微型端口驱动程序的控制下的所有内容：

-   禁用网络适配器上的中断和 DMA 引擎。

-   停止网络适配器上的接收引擎。

-   不要解除分配或修改与挂起的接收指示关联的接收描述符和数据包缓冲区。

-   取消所有 NDIS 计时器。

**请注意**，在总线驱动程序将网络适配器转换到 D3 状态后，小型使用驱动程序无法访问网络适配器  。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>过渡到完整电源状态（D0）

当微型端口驱动程序处理 OID\_PNP\_设置的请求时，必须\_将网络适配器的接收引擎还原到接收引擎在将适配器转换为低功耗状态之前所处的相同状态，才能恢复到该状态。

**请注意**  微型端口驱动程序不得访问或更改与挂起的接收指示关联的任何接收缓冲区。

 

仅当 NDIS 在转换到低功耗状态之前调用了驱动程序的[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)函数时，ndis 才会在转换到全电源状态后调用微型端口驱动程序的[*MiniportRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)函数。

**请注意**  中间驱动程序必须始终将**NDIS\_状态返回\_成功**，\_PNP\_设置\_电源。 中间驱动程序绝不应将 OID 传播\_PNP\_将\_电源请求设置为底层微型端口驱动程序。

 

## <a name="return-status-codes"></a>返回状态代码


微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数为此请求返回以下值之一：

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数来成功请求，同时传递 NDIS_STATUS_SUCCESS 的<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
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
<td><p>支持 NDIS 5.1 和 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)

[*MiniportRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)

[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)

[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)

[**NDIS\_设备\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

 

 




