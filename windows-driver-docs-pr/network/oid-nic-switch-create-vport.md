---
title: OID_NIC_SWITCH_CREATE_VPORT
description: 过量驱动程序发出 OID_NIC_SWITCH_CREATE_VPORT 的对象标识符（OID）方法请求，以在网络适配器的 NIC 交换机上创建非默认的虚拟端口（VPort）。
ms.assetid: 31109117-2242-40E0-B215-0FAE014B2035
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_VPORT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f525f3da17bb5316f06db571c1de70a9329818f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844097"
---
# <a name="oid_nic_switch_create_vport"></a>OID\_NIC\_交换机\_CREATE\_VPORT


过量驱动程序发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_CREATE\_VPORT 在网络适配器的 NIC 交换机上创建非默认的虚拟端口（VPort）。 此 OID 方法请求还会将创建的 VPort 附加到网络适配器的 PCI Express （PCIe）物理功能（PF）或之前分配的 PCIe 虚拟函数（VF）。

过量驱动程序将此 OID 方法请求颁发给网络适配器的 PF 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_SWITCH\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。

<a name="remarks"></a>备注
-------

覆盖驱动程序将[**NDIS\_NIC 初始化\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构，以及有关要创建的非默认 VPORT 的配置信息。 配置信息包括非默认 VPort 附加到的 PCIe 函数以及非默认 VPort 的队列对数。

当对 PF 小型端口驱动程序发出 OID 请求时，驱动程序会分配与指定的非默认 VPort 关联的硬件和软件资源。 成功分配所有资源后，PF 微型端口驱动程序会通过从[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)返回 NDIS\_\_状态，成功完成 OID。

如果 OID\_NIC\_交换机\_CREATE\_VPORT 请求成功完成，则 PF 微型端口驱动程序和过量驱动程序必须保留非默认 VPort 的**VPortId**值才能执行后续操作。 在以下操作过程中将使用**VPortId**值：

-   NDIS 和过量驱动程序使用**VPortId**值标识与此 VPort 相关的后续 OID 请求中的非默认 VPort，如[oid\_nic\_switch\_VPort\_参数](oid-nic-switch-vport-parameters.md)和[OID\_nic\_VPort\_DELETE\_](oid-nic-switch-delete-vport.md)。

-   在发送操作期间，NDIS 指定**VPortId**值以标识从中发送数据包的 VPort。 此值在带外（OOB） [**NDIS\_NET\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)中指定，\_筛选[网络\_缓冲区\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)结构的\_信息数据。

-   在接收操作期间，PF 微型端口驱动程序指定将数据包转发到的**VPortId**值。 此值还在 OOB [**NDIS\_NET\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)中指定，\_筛选[网络\_缓存\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)结构\_信息数据。

有关详细信息，请参阅[创建虚拟端口](https://docs.microsoft.com/windows-hardware/drivers/network/creating-a-virtual-port)。

**请注意**  默认 VPort 始终存在，并且不是通过 OID 的 oid 请求\_NIC\_SWITCH\_创建\_VPort。 默认的 VPort 的标识符\_默认\_VPORT\_ID。 当 PF 微型端口驱动程序创建 NIC 交换机时，驱动程序会自动将默认 VPort 附加到网络适配器的 PF。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 或 PF 微型端口驱动程序返回 OID 的 OID 方法请求之一的以下状态代码之一\_NIC\_SWITCH\_CREATE\_开关。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)"><strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[ **\_交换机\_参数的 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[NET\_缓冲区\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_交换机\_参数](oid-nic-switch-parameters.md)

[OID\_NIC\_SWITCH\_VPORT\_参数](oid-nic-switch-vport-parameters.md)

 

 




