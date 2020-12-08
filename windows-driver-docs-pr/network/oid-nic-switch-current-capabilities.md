---
title: OID_NIC_SWITCH_CURRENT_CAPABILITIES
description: 过量驱动程序发出对象标识符 (OID) 查询请求 OID_NIC_SWITCH_CURRENT_CAPABILITIES 获取网络适配器中 NIC 交换机当前启用的硬件功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d5c70f9dce882ec565f2612153d2ffac7707bf7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839873"
---
# <a name="oid_nic_switch_current_capabilities"></a>OID \_ NIC \_ 交换机 \_ 当前 \_ 功能


过量驱动程序发出对象标识符 (OID) 请求 OID \_ nic \_ switch \_ 当前 \_ 功能，以获取网络适配器中 NIC 交换机当前启用的硬件功能。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

从 NDIS 6.20 开始，微型端口驱动程序会在调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，为网络适配器提供当前启用的 NIC 交换机硬件功能。 驱动程序使用 NIC 交换机硬件功能初始化 [**ndis \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，并将 [**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的 **CurrentNicSwitchCapabilities** 成员设置为指向 **NDIS \_ NIC \_ 交换机 \_ 功能** 结构的指针。 然后，小型端口驱动程序将调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，并将 *MiniportAttributes* 参数设置为指向 **NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性** 结构的指针。

**注意**  从 NDIS 6.30 开始，支持单个根 i/o 虚拟化 (SR-IOV) 接口的微型端口驱动程序必须注册 NIC 交换机的已启用硬件功能。 驱动程序通过调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)注册这些功能。

 

过量协议和筛选器驱动程序不必发出 oid \_ NIC \_ 交换机 \_ 当前功能的 oid 查询请求 \_ 。 NDIS 按以下方式将网络适配器的当前启用的 NIC 交换机硬件功能提供给这些驱动程序：

-   在绑定操作过程中，NDIS 会将基础网络适配器的当前启用的 NIC 交换机硬件功能报告到 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **NicSwitchCapabilities** 成员中的过量协议驱动程序。

-   NDIS 报告底层网络适配器的当前启用的 NIC 交换机硬件功能，用于在附加操作期间覆盖 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构的 **NicSwitchCapabilities** 成员中的驱动程序。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID \_ NIC \_ 交换机 \_ 当前 \_ 功能请求以获取微型端口驱动程序的 oid 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ NIC \_ SWITCH \_ 当前 \_ 功能请求时，它将返回以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>) 。 微型端口驱动程序必须设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>由于其他原因，请求失败。</p></td>
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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

