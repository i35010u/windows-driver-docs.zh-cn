---
title: OID_SRIOV_RESET_VF
description: 过量驱动程序发出 (OID 的对象标识符) 设置 OID_SRIOV_RESET_VF 的请求，以在支持单一根 i/o 虚拟化的网络适配器上重置指定的 PCI Express (PCIe) 虚拟函数 (VF) 。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_RESET_VF 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1af835c6ba77dee089311c56cbf6534239e04624
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812979"
---
# <a name="oid_sriov_reset_vf"></a>OID \_ SRIOV \_ 重置 \_ VF


过量驱动程序发出 (OID 的对象标识符) \_ \_ \_ 在支持单一根 i/o 虚拟化的网络适配器上，使用 oid SRIOV reset vf 重置指定 PCI Express (PCIe) 虚函数 (VF) 。 过量驱动程序发出此 OID 集请求到 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 网络适配器。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ SRIOV \_ 重置 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构的指针。 过量驱动程序通过此结构的 **VFId** 成员指定要重置的 VF 的标识符。

<a name="remarks"></a>备注
-------

可以通过 PCI Express (PCIe) 功能级别重置 (FLR) 重置 VF。 由于 FLR 请求是一项特权操作，因此只能由 Hyper-v 父分区的管理操作系统中运行的 PF 微型端口驱动程序执行。 在管理操作系统中运行的过量驱动程序将收到 FLR 请求的通知，并 \_ \_ \_ 向 PF 微型端口驱动程序发出 oid SRIOV 重置 VF 的 oid 请求。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 [**NDIS \_ SRIOV \_ 重置 \_ Vf \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构的 **VFId** 成员指定的 VF 是否包含之前已分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   Reset 操作必须只影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

有关详细信息，请参阅 [重置虚函数](./resetting-a-virtual-function.md)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ SRIOV \_ 重置 VF 的 set 请求，PF 微型端口驱动程序返回以下状态代码之一 \_ 。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_RESET_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)"><strong>NDIS_SRIOV_RESET_VF_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 PF 微型端口驱动程序必须设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ 重置 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

