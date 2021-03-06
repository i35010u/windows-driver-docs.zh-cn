---
title: OID_SRIOV_SET_VF_POWER_STATE
description: 过量驱动程序会 (OID 发出对象标识符) 设置 OID_SRIOV_SET_VF_POWER_STATE 的请求，以更改网络适配器上指定 PCI Express (PCIe) 虚拟函数 (虚拟功能) 的电源状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_SET_VF_POWER_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 58156543462aed4b30923c0989ce34ffccd380b0
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248801"
---
# <a name="oid_sriov_set_vf_power_state"></a>OID \_ SRIOV \_ SET \_ VF \_ 电源 \_ 状态


过量驱动程序发出 (OID 的对象标识符) 设置 OID 的请求 \_ ， \_ \_ \_ \_ 以更改网络适配器上指定 PCI Express (PCIE) 虚函数 (VF 的电源状态。 由于更改电源状态是特权操作，因此过量驱动程序会在网络适配器上向 PCIe 物理功能 (PF) 的微型端口驱动程序发出此 OID 设置请求。 然后，PF 微型端口驱动程序将设置 VF 上指定的电源状态。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ SRIOV \_ SET \_ VF \_ 电源 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构的指针。

<a name="remarks"></a>备注
-------

当向此 OID 集请求颁发了 PF 微型端口驱动程序时，必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 [**NDIS \_ SRIOV \_ SET \_ vf \_ 电源 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构的 **VFId** 成员指定的 VF 是否具有以前分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果指定的 VF 未处于已分配状态，则驱动程序必须使 OID 请求失败。

-   电源状态操作只能影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

有关详细信息，请参阅 [设置虚拟功能的电源状态](./setting-the-power-state-of-a-virtual-function.md)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 oid \_ SRIOV \_ set \_ VF \_ 电源 \_ 状态的 oid 设置请求返回以下状态之一。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)"><strong>NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 PF 微型端口驱动程序必须设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ SRIOV \_ 设置 \_ VF \_ 电源 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

