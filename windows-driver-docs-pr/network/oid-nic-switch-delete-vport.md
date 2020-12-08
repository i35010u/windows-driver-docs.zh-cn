---
title: OID_NIC_SWITCH_DELETE_VPORT
description: 过量驱动程序会 (OID 发出对象标识符) 设置 OID_NIC_SWITCH_DELETE_VPORT 的请求，以删除以前在网络适配器的 NIC 交换机上创建的非默认虚拟端口 (VPort) 。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_DELETE_VPORT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3c5e600a0d23b8b7814bffdb7105cbb8b6f5db4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795945"
---
# <a name="oid_nic_switch_delete_vport"></a>OID \_ NIC \_ 交换机 \_ 删除 \_ VPORT


过量驱动程序会 (OID 发出对象标识符) 设置 OID \_ NIC \_ 交换机 \_ delete \_ VPORT，以删除以前在网络适配器的 NIC 交换机上创建 (VPORT) 的非默认虚拟端口。 过量驱动程序可以通过发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPort](oid-nic-switch-create-vport.md)的 oid 方法请求来删除以前创建的 VPort。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 集请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ SWITCH \_ DELETE \_ VPORT \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构的指针。

<a name="remarks"></a>备注
-------

过量驱动程序（如协议或筛选器驱动程序）只能删除先前创建的非默认 VPort。 过量驱动程序通过发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPort](oid-nic-switch-create-vport.md)的 Oid 方法请求来创建一个 VPort。

当 PF 微型端口驱动程序收到 OID \_ NIC SWITCH DELETE VPORT 的 oid 请求时 \_ \_ \_ ，驱动程序必须释放为指定的 VPORT 分配的硬件和软件资源。

有关详细信息，请参阅 [删除虚拟端口](./deleting-a-virtual-port.md)。

**注意**  只有非默认 VPorts 可以通过 oid \_ NIC \_ SWITCH \_ DELETE VPORT 的 oid 请求显式删除 \_ 。 当 PF 微型端口驱动程序删除默认 NIC 交换机时，会隐式删除默认 VPort。 有关详细信息，请参阅 [删除 NIC 交换机](./deleting-a-nic-switch.md)。

 

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID \_ NIC \_ 开关 \_ DELETE VPORT 返回以下状态代码之一 \_ 。

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
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>) 。 PF 微型端口驱动程序必须设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ NIC \_ 交换机 \_ 删除 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)

[OID \_ NIC \_ 交换机 \_ 删除 \_ 开关](oid-nic-switch-delete-switch.md)

