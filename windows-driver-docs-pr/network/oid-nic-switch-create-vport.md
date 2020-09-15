---
title: OID_NIC_SWITCH_CREATE_VPORT
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_NIC_SWITCH_CREATE_VPORT，以便在网络适配器的 NIC 交换机上创建非默认的虚拟端口 (VPort) 。
ms.assetid: 31109117-2242-40E0-B215-0FAE014B2035
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_VPORT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: afb40fff15053d4954f86f2b072a6a26e02e3afa
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106056"
---
# <a name="oid_nic_switch_create_vport"></a>OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT


过量驱动程序发出对象标识符)  (oid \_ NIC \_ 交换机 \_ create \_ VPORT 在网络适配器的 nic 交换机上创建非默认的虚拟端口 (VPORT) 。 此 OID 方法请求还会将创建的 VPort 附加到网络适配器的 PCI Express (PCIe) 物理功能 (PF) 或以前分配的 PCIe 虚拟函数 (VF) 。

过量驱动程序将此 OID 方法请求颁发给网络适配器的 PF 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的指针。

<a name="remarks"></a>备注
-------

过量驱动程序将 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构初始化为有关要创建的非默认 VPORT 的配置信息。 配置信息包括非默认 VPort 附加到的 PCIe 函数以及非默认 VPort 的队列对数。

当对 PF 小型端口驱动程序发出 OID 请求时，驱动程序会分配与指定的非默认 VPort 关联的硬件和软件资源。 成功分配所有资源后，PF 微型端口驱动程序会通过 \_ 从 MiniportOidRequest 返回 NDIS 状态成功完成 OID \_ 。 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

如果 OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT 请求成功完成，则 PF 微型端口驱动程序和过量驱动程序必须保留非默认 VPORT 的 **VPortId** 值，以便执行后续操作。 在以下操作过程中将使用 **VPortId** 值：

-   NDIS 和过量驱动程序使用 **VPortId** 值标识与此 VPort 相关的后续 oid 请求中的非默认 VPort，如 [oid \_ nic \_ switch \_ VPort \_ 参数](oid-nic-switch-vport-parameters.md) 和 [oid \_ nic \_ switch \_ DELETE \_ VPort](oid-nic-switch-delete-vport.md)。

-   在发送操作期间，NDIS 指定 **VPortId** 值以标识从中发送数据包的 VPort。 此值在带外 (OOB) [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info) 数据的 [网络 \_ 缓冲区 \_ 列表](./net-buffer-list-structure.md) 结构内指定。

-   在接收操作期间，PF 微型端口驱动程序指定将数据包转发到的 **VPortId** 值。 此值还在[网络 \_ 缓冲区 \_ 列表](./net-buffer-list-structure.md)结构的 OOB [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)数据中指定。

有关详细信息，请参阅 [创建虚拟端口](./creating-a-virtual-port.md)。

**注意**   默认 VPort 始终存在，不会通过 OID \_ NIC \_ 交换机 \_ CREATE VPort 的 oid 请求创建 \_ 。 默认 VPort 具有 NDIS \_ default VPort ID 的标识符 \_ \_ 。 当 PF 微型端口驱动程序创建 NIC 交换机时，驱动程序会自动将默认 VPort 附加到网络适配器的 PF。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序为 OID \_ NIC \_ 交换机 \_ 创建开关的 oid 方法请求返回以下状态之一 \_ 。

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
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>) 。 PF 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>另请参阅


****
[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS \_ NIC \_ SWITCH \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[网络 \_ 缓冲区 \_ 列表](./net-buffer-list-structure.md)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ NIC \_ 交换机 \_ 删除 \_ VPORT](oid-nic-switch-delete-vport.md)

[OID \_ NIC \_ 交换机 \_ 参数](oid-nic-switch-parameters.md)

[OID \_ NIC \_ SWITCH \_ VPORT \_ 参数](oid-nic-switch-vport-parameters.md)

