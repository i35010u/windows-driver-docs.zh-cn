---
title: OID_SRIOV_SET_VF_POWER_STATE
description: 过量驱动程序发出 OID_SRIOV_SET_VF_POWER_STATE 的对象标识符（OID）设置请求，以更改网络适配器上指定 PCI Express （PCIe）虚拟功能（VF）的电源状态。
ms.assetid: 9723518E-2312-48F9-820A-19F5567A33DB
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_SET_VF_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 06e2c85565a0f5ae3feba00cec75982bab1a8102
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843978"
---
# <a name="oid_sriov_set_vf_power_state"></a>OID\_SRIOV\_设置\_VF\_POWER\_状态


过量驱动程序发出 OID\_的对象标识符（OID）设置请求\_设置\_VF\_POWER\_状态，以更改网络适配器上指定 PCI Express （PCIe）虚拟功能（VF）的电源状态。 由于更改电源状态是特权操作，因此过量驱动程序将此 OID 集请求颁发给网络适配器上 PCIe 物理功能（PF）的微型端口驱动程序。 然后，PF 微型端口驱动程序将设置 VF 上指定的电源状态。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_设置\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)\_\_\_参数结构的指针。

<a name="remarks"></a>备注
-------

当向此 OID 集请求颁发了 PF 微型端口驱动程序时，必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 VF [ **\_设置\_VF\_POWER\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构，具有以前的资源分配. 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果指定的 VF 未处于已分配状态，则驱动程序必须使 OID 请求失败。

-   电源状态操作只能影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

有关详细信息，请参阅[设置虚拟功能的电源状态](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-power-state-of-a-virtual-function)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序返回 OID\_SRIOV 的 OID 集的以下状态代码之一\_设置\_VF\_POWER\_状态。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)"><strong>NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
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

[**NDIS\_SRIOV\_设置\_VF\_POWER\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

 

 




