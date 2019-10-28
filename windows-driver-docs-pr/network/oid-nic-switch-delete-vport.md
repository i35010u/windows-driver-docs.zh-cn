---
title: OID_NIC_SWITCH_DELETE_VPORT
description: 过量驱动程序发出 OID_NIC_SWITCH_DELETE_VPORT 的对象标识符（OID）设置请求，以删除以前在网络适配器的 NIC 交换机上创建的非默认虚拟端口（VPort）。
ms.assetid: D762035C-33AC-4579-8EA0-6A422AE4CA76
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_DELETE_VPORT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 12f18d5992499e64ce090d9e37bf3ae97ce0eed7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844092"
---
# <a name="oid_nic_switch_delete_vport"></a>OID\_NIC\_交换机\_DELETE\_VPORT


过量驱动程序发出 OID\_NIC 的对象标识符（OID）设置请求\_交换机\_DELETE\_VPORT 删除以前在网络适配器的 NIC 交换机上创建的非默认虚拟端口（VPort）。 过量驱动程序可以删除以前创建的 VPort，该方法仅\_\_NIC 发出 oid 方法请求， [\_CREATE\_VPort](oid-nic-switch-create-vport.md)。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 支持单一根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 集请求。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_交换机\_DELETE\_VPORT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构。

<a name="remarks"></a>备注
-------

过量驱动程序（如协议或筛选器驱动程序）只能删除先前创建的非默认 VPort。 过量驱动程序通过\_\_NIC 发出 oid 方法请求， [\_CREATE\_VPort](oid-nic-switch-create-vport.md)，来创建一个 VPort。

当 PF 微型端口驱动程序接收 OID\_NIC\_交换机\_DELETE\_VPORT 的 OID 请求时，驱动程序必须释放为指定的 VPort 分配的硬件和软件资源。

有关详细信息，请参阅[删除虚拟端口](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-virtual-port)。

**请注意**  只能通过 OID\_NIC\_开关\_DELETE\_VPORT 的 oid 请求显式删除非默认 VPorts。 当 PF 微型端口驱动程序删除默认 NIC 交换机时，会隐式删除默认 VPort。 有关详细信息，请参阅[删除 NIC 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)。

 

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 oid\_NIC\_交换机\_DELETE\_VPORT 返回以下状态代码之一。

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
<td><p>PF 微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_DELETE\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_DELETE\_开关](oid-nic-switch-delete-switch.md)

 

 




