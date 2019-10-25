---
title: OID_SRIOV_RESET_VF
description: 过量驱动程序发出 OID_SRIOV_RESET_VF 的对象标识符（OID）设置请求，以在支持单一根 i/o 虚拟化的网络适配器上重置指定的 PCI Express （PCIe）虚拟功能（VF）。
ms.assetid: 7D5EB64B-3345-478A-8D42-192939C0B9C2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_RESET_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37fdf0a0cf1f6f98941c9ccb5f3e26b53822f9ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843980"
---
# <a name="oid_sriov_reset_vf"></a>OID\_SRIOV\_RESET\_VF


过量驱动程序发出 OID\_SRIOV 的对象标识符（OID）设置请求\_RESET\_VF 重置支持单一根 i/o 虚拟化的网络适配器上的指定 PCI Express （PCIe）虚拟功能（VF）。 过量驱动程序发出此 OID 集请求到网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_重置\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构的指针。 过量驱动程序通过此结构的**VFId**成员指定要重置的 VF 的标识符。

<a name="remarks"></a>备注
-------

可以通过 PCI Express （PCIe）功能级别重置（FLR）重置 VF。 由于 FLR 请求是一项特权操作，因此只能由 Hyper-v 父分区的管理操作系统中运行的 PF 微型端口驱动程序执行。 在管理操作系统中运行的过量驱动程序将收到 FLR 请求的通知，并发出 oid\_SRIOV 的 oid 集请求\_将\_VF 重置到 PF 微型端口驱动程序。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 vf 是否[ **\_RESET\_vf\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构）是否具有以前分配的资源。 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   Reset 操作必须只影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

有关详细信息，请参阅[重置虚函数](https://docs.microsoft.com/windows-hardware/drivers/network/resetting-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序返回\_SRIOV 的设置请求的以下状态代码之一\_重置\_VF。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_RESET_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)"><strong>NDIS_SRIOV_RESET_VF_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 PF 微型端口驱动程序必须设置<strong>数据。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_RESET\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

 

 




