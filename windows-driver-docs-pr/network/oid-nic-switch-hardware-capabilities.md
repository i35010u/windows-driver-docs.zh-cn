---
title: OID_NIC_SWITCH_HARDWARE_CAPABILITIES
description: 过量驱动程序会发出对象标识符 (OID) 查询请求 OID_NIC_SWITCH_HARDWARE_CAPABILITIES 获取网络适配器中 NIC 交换机的硬件功能。
ms.assetid: 2c417a16-68e1-4754-88a5-8bac4653e05d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_HARDWARE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f8ff80e10d672426c7b7d10d98434785ce6d4e32
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218369"
---
# <a name="oid_nic_switch_hardware_capabilities"></a>OID \_ NIC \_ 交换机 \_ 硬件 \_ 功能


过量驱动程序) OID nic 交换机硬件功能 (OID 发出对象标识符 \_ \_ \_ \_ ，以获取网络适配器中 NIC 交换机的硬件功能。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构包含有关网络适配器上 NIC 交换机的硬件功能的信息。 这些功能可能包括 INF 文件设置当前禁用的硬件功能，或通过 " **高级** 属性" 页当前禁用的硬件功能。

**注意**   指定 NIC 交换机的所有功能都通过 oid NIC 交换机硬件功能的 OID 查询请求 \_ 返回 \_ \_ \_ ，而不考虑是否启用或禁用功能。

 

从 NDIS 6.20 开始，微型端口驱动程序会在调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时提供 NIC 交换机硬件功能。 驱动程序使用 NIC 交换机硬件功能初始化[**ndis \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，并将[**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的**HardwareNicSwitchCapabilities**成员设置为指向**NDIS \_ NIC \_ 交换机 \_ 功能**结构的指针。 然后，小型端口驱动程序将调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，并将 *MiniportAttributes* 参数设置为指向 **NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性** 结构的指针。

**注意**   从 NDIS 6.30 开始，支持单个根 i/o 虚拟化 (SR-IOV) 接口的微型端口驱动程序必须注册 NIC 交换机的硬件功能。 驱动程序通过调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)注册这些功能。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ \_ 对微型端口驱动程序的 oid NIC 交换机硬件功能请求的 oid 查询请求 \_ ，并返回以下状态代码之一：

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>) 。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

