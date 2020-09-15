---
title: OID_NIC_SWITCH_VPORT_PARAMETERS
description: 过量驱动程序可以获取 NIC 交换机上的虚拟端口 (VPort) 的参数，这些参数在支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器上创建。
ms.assetid: B22C760E-F2B0-4774-A532-4044C679CD64
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_VPORT_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 463abaec2d6c48a126595f23e4e672f38f307b73
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106012"
---
# <a name="oid_nic_switch_vport_parameters"></a>OID \_ NIC \_ SWITCH \_ VPORT \_ 参数


过量驱动程序可以获取 NIC 交换机上的虚拟端口 (VPort) 的参数，这些参数在支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器上创建。 驱动程序) OID NIC SWITCH VPORT 参数的方法请求 (OID 发出对象标识符 \_ \_ \_ \_ ，以获取这些参数。

过量驱动程序发出 oid \_ NIC SWITCH VPORT 参数的 oid 集请求 \_ \_ \_ ，以设置附加到网络适配器的 NIC 交换机的指定 VPORT 的配置参数。 这些 OID 集请求将颁发给网络适配器 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序。 对于支持 (SR-IOV) 接口的单个根 i/o 虚拟化的 PF 微型端口驱动程序，这些 OID 设置请求是必需的。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的指针。

过量驱动程序通过将[**NDIS \_ NIC \_ SWITCH \_ VPort \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的**VPortId**成员设置为与 VPort 关联的标识符来指定 OID 方法或 set 请求的 VPort。 过量驱动程序通过以下方式之一获取 VPort 标识符：

-   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](oid-nic-switch-create-vport.md)。

-   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

<a name="remarks"></a>注解
-------

OID \_ NIC \_ SWITCH \_ VPORT \_ 参数可用于 [oid 方法请求](#oid-method-requests) 或 [oid 设置请求](#oid-set-requests)。

### <a name="handling-oid-method-requests-of-oid_nic_switch_vport_parameters"></a><a href="" id="oid-method-requests"></a>处理 OID \_ NIC \_ SWITCH \_ VPORT \_ 参数的 oid 方法请求

过量驱动程序发出 oid \_ NIC switch VPORT 参数的 oid 方法请求 \_ \_ \_ ，以查询附加到网络适配器的 NIC 交换机的 VPORT 的当前配置参数。 过量驱动程序通过将[**NDIS \_ NIC \_ SWITCH \_ VPort \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的**VPortId**成员设置为 VPort 标识符来指定要查询的 VPort。

NDIS 处理 \_ \_ \_ \_ 适用于微型端口驱动程序的 oid NIC 交换机 VPORT 参数的 oid 方法请求。 NDIS 返回从 [oid \_ nic \_ switch \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md) 和 [OID \_ nic \_ 交换机 \_ 枚举 \_ VPORTS](oid-nic-switch-enum-vports.md)的以前 oid 请求获取的信息。

成功从 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的指针。 此结构包含指定开关的配置参数。

有关详细信息，请参阅 [查询虚拟端口的参数](./querying-the-parameters-of-a-virtual-port.md)。

### <a name="handling-oid-set-requests-of-oid_nic_switch_vport_parameters"></a><a href="" id="oid-set-requests"></a>处理 oid \_ NIC \_ SWITCH \_ VPORT \_ 参数的 oid 集请求

过量驱动程序发出 oid \_ NIC SWITCH VPORT 参数的 oid 集请求 \_ \_ \_ ，以更改附加到网络适配器的 NIC 交换机的 VPORT 的当前配置参数。 此 OID 请求可用于更新默认值和非默认 VPorts 的参数。

只能更改 VPort 的配置参数的有限子集。 过量驱动程序通过设置 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构的以下成员来指定要更改的参数：

1.  **VPortId**成员设置为将更改其参数的 VPort 的标识符。

2.  在 \_ \_ flags 成员中设置相应的 NDIS NIC 交换机 \_ VPORT \_ 参数 \_ *Xxx* \_ 更改**Flags**标志。 仅当在 Ntddndis 中定义了相应的 NDIS nic 交换机参数 Xxx changed 标志时，才能更改[**NDIS \_ nic \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的成员 \_ \_ \_ \_ *Xxx* \_ 。

3.  [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的相应成员是用要更改的 VPORT 配置参数设置的。

当 PF 微型端口驱动程序接收 OID NIC SWITCH VPORT 参数的 OID 集请求后 \_ \_ \_ \_ ，该驱动程序将用配置参数配置硬件。 此驱动程序只能在 \_ \_ \_ \_ \_ *Xxx* \_ [**ndis \_ nic \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的**flags**成员中更改由 ndis nic 交换机 VPORT 参数 Xxx 更改的标志。

有关详细信息，请参阅 [设置虚拟端口的参数](./setting-the-parameters-of-a-virtual-port.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序为 OID \_ NIC \_ SWITCH \_ VPORT 参数的设置或方法 oid 请求返回以下状态代码 \_ 。

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
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 或 PF 微型端口驱动程序设置 <strong>数据。METHOD_INFORMATION。</strong> (OID 方法请求) 或数据的 BytesNeeded 成员 <strong>。SET_INFORMATION。BytesNeeded</strong> 成员 () 在 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中，将其设置为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ NIC \_ SWITCH \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)

[OID \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](oid-nic-switch-enum-vports.md)

