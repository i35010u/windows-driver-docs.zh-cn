---
title: OID_NIC_SWITCH_ALLOCATE_VF
description: 过量驱动程序发出 OID_NIC_SWITCH_ALLOCATE_VF 的对象标识符（OID）方法请求，以分配 PCI Express （PCIe）虚拟功能（VF）的资源。
ms.assetid: CB88CE0C-705F-406B-90FE-FB206D6F4864
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ALLOCATE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8da9ace40d3bfb1b7458475446dc645e6ca20af2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844103"
---
# <a name="oid_nic_switch_allocate_vf"></a>OID\_NIC\_交换机\_分配\_VF


过量驱动程序发出 OID\_\_的对象标识符（OID）方法请求，\_分配\_VF 来分配 PCI Express （PCIe）虚拟功能（VF）的资源。 VF 在支持单根 i/o 虚拟化（SR-IOV）接口的网络适配器上公开。

过量驱动程序将此 OID 方法请求颁发给网络适配器的 PCIe 物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_\_NIC 的指针，\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

<a name="remarks"></a>备注
-------

当驱动程序处理 OID 的对象标识符（OID）方法请求时，PF 微型端口驱动程序会为 VF 分配软件资源\_NIC\_交换机\_分配\_VF。 即使已为 VF 分配硬件资源，也会将其视为 nonoperational，直到 PF 微端口驱动程序成功完成 OID\_NIC\_交换机\_分配\_VF。

有关如何分配 VF 资源的详细信息，请参阅为[虚拟函数分配资源](https://docs.microsoft.com/windows-hardware/drivers/network/allocating-resources-for-a-virtual-function)。

**请注意**  在过量驱动程序为 vf 请求分配资源后，该驱动程序是唯一可以请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](oid-nic-switch-free-vf.md)来释放 VF 资源。 在可以停止过量驱动程序之前，它必须释放由驱动程序的 OID\_NIC 分配的每个 VF 的资源\_交换机\_分配\_VF 请求。

 

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序将为 oid\_NIC\_交换机\_分配\_VF 的 OID 方法请求之一返回以下状态代码之一。

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
<td><p>PF 微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_使\_RID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[**NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[OID\_NIC\_交换机\_免费\_VF](oid-nic-switch-free-vf.md)

 

 




