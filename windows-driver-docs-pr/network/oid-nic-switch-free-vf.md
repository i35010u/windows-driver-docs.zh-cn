---
title: OID_NIC_SWITCH_FREE_VF
description: 过量驱动程序发出 OID_NIC_SWITCH_FREE_VF 的对象标识符（OID）设置请求，以释放网络适配器 PCI Express （PCIe）虚拟功能（VF）的资源。过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 支持单一根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 集请求。
ms.assetid: B1A72D34-286A-4A70-8BE3-F21324B92187
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_FREE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8da71ffdc8d9d17094220f0594e26d8b00828143
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844084"
---
# <a name="oid_nic_switch_free_vf"></a>OID\_NIC\_交换机\_免费\_VF


过量驱动程序发出 OID\_\_NIC 的对象标识符（OID）设置请求，\_免费\_VF，以释放网络适配器 PCI Express （PCIe）虚拟功能（VF）的资源。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 支持单一根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 集请求。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_\_NIC 的指针，\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。

过量驱动程序指定要通过此结构的**VFId**成员释放的 VF 的标识符。 此驱动程序从 Oid 的早期 OID 方法请求中获取此标识符[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

<a name="remarks"></a>备注
-------

过量驱动程序发出 oid\_NIC 的 oid 集请求\_交换机\_免费\_VF 来释放 VF 的资源。 之前已通过 oid 的 OID 方法请求对这些资源进行了分配[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

有关如何释放 VF 资源的详细信息，请参阅[释放虚拟功能的资源](https://docs.microsoft.com/windows-hardware/drivers/network/freeing-resources-for-a-virtual-function)。

**请注意**  一旦过量驱动程序请求了用于 vf 的资源分配，该驱动程序就是可以请求为同一 VF 释放资源的唯一组件。 过量驱动程序必须发出 oid\_NIC 的 OID 集请求\_交换机\_免费\_VF 来释放 VF 资源。 在可以停止过量驱动程序之前，它必须释放由驱动程序的 OID\_NIC 分配的每个 VF 的资源[\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)请求。

 

### <a name="return-status-codes"></a>返回状态代码

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数（为<em>STATUS</em>参数传递<strong>NDIS_STATUS_SUCCESS</strong> ）成功执行请求。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a>函数。</p></td>
</tr>
</tbody>
</table>

 

NDIS 为此请求返回以下状态代码之一：

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
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_FREE_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)"><strong>NDIS_NIC_SWITCH_FREE_VF_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。 例如， <strong>VFId</strong>成员可能指定尚未分配或具有尚未删除的 VPORTS 的 VF。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太小。 NDIS 设置<strong>数据。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_NIC\_交换机\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_交换机\_DELETE\_开关](oid-nic-switch-delete-switch.md)

 

 




