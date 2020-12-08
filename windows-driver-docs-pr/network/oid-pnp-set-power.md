---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_SET_POWER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 26efec0328873f8770668bc01616c9856c1dac6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827527"
---
# <a name="oid_pnp_set_power"></a>OID \_ PNP \_ 设置 \_ 电源





OID \_ PNP \_ 集 \_ 电源 oid 通知小型端口驱动程序，其基础网络适配器将转换为 *InformationBuffer* 中指定的设备电源状态。 设备电源状态指定为下列 [**NDIS \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state) 值之一：

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

OID \_ pnp \_ 集 \_ 电源请求可能位于 [oid \_ pnp \_ 查询 \_ 电源](oid-pnp-query-power.md) 请求之前。

从 NDIS 6.30 开始，如果满足以下条件，NDIS 将不会在驱动程序堆栈中暂停和重新启动 NDIS 驱动程序：

-   基础微型端口驱动程序在 [**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构中设置 **ndis \_ 微型端口 \_ 属性 " \_ \_ \_ \_ 挂起时暂停**" 标志。 驱动程序在其对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数的调用中传递指向此结构的指针。

-   附加到微型端口驱动程序的所有过量筛选器驱动程序都支持 NDIS 6.30 或更高版本的 NDIS。

-   绑定到微型端口驱动程序的所有过量协议驱动程序都支持 NDIS 6.30 或更高版本的 NDIS。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>转换到 Low-Power 状态 (D1-D3) 

当微型端口驱动程序处理 OID \_ PNP 集电源的 set 请求 \_ \_ 转换为低功率状态时，它必须执行以下操作：

-   为指示的网络设备电源状态充分准备网络适配器。 微型端口驱动程序执行的任务是与设备相关的。

-   等待对 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数的调用返回。

-   等待网络适配器处理的发送请求完成。 完成后，微型端口驱动程序必须调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数。 驱动程序应将每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 **状态** 成员设置为相应的 NDIS \_ 状态 \_ *Xxx* 值。

-   通过调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 函数完成所有挂起的发送请求。 驱动程序必须将每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 **状态** 成员设置为 **NDIS \_ 状态 \_ 低 \_ 电源 \_ 状态**。

-   通过调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)函数，立即拒绝对其 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数发出的所有新发送请求。 驱动程序必须将每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 **状态** 成员设置为 **NDIS \_ 状态 \_ 低 \_ 电源 \_ 状态**。

支持 NDIS 6.30 和更高版本的 NDIS 的微型端口驱动程序还必须执行以下操作：

-   不等待通过调用 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) 函数来完成挂起的接收指示。 此外，微型端口驱动程序不得为等待完成的任何数据包更改 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构或数据。

-   \_ \_ \_ 从暂停或正在运行的适配器状态中，将 OID PNP 集电源请求处理为低功耗状态。 有关这些状态的详细信息，请参阅 [微型端口适配器状态和操作](./miniport-adapter-states-and-operations.md)。

在网络适配器转换到 D3 状态之前，微型端口驱动程序必须通过执行以下任务来关闭微型端口驱动程序的控制下的所有内容：

-   禁用网络适配器上的中断和 DMA 引擎。

-   停止网络适配器上的接收引擎。

-   不要解除分配或修改与挂起的接收指示关联的接收描述符和数据包缓冲区。

-   取消所有 NDIS 计时器。

**注意**  当总线驱动程序将网络适配器转换为 D3 状态后，微型端口驱动程序无法访问网络适配器。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>转换到 Full-Power 状态 (D0) 

当微型端口驱动程序处理 OID \_ PNP 集电源的 set 请求 \_ \_ 转换为全功能状态时，它必须将网络适配器的接收引擎还原到接收引擎在将适配器转换为低功耗状态之前所处的状态。

**注意**  微型端口驱动程序不得访问或更改与挂起的接收指示关联的任何接收缓冲区。

 

仅当 NDIS 在转换到低功耗状态之前调用了驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)函数时，ndis 才会在转换到全电源状态后调用微型端口驱动程序的 [*MiniportRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)函数。

**注意**  中间驱动程序必须始终将 **NDIS \_ 状态 \_ 成功** 返回到 OID \_ PNP \_ 设置电源的查询 \_ 。 中间驱动程序绝不应将 OID \_ PNP \_ 集 \_ 电源请求传播到基础微型端口驱动程序。

 

## <a name="return-status-codes"></a>返回状态代码


微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数为此请求返回以下值之一：

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a> 函数来成功请求，同时传递 NDIS_STATUS_SUCCESS 的 <em>状态</em> 参数。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)

[*MiniportRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)

[*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)

[*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)

[**NDIS \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

