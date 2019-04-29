---
title: OID_SRIOV_SET_VF_POWER_STATE
description: 基础驱动程序发出的对象标识符 (OID) 组请求的 OID_SRIOV_SET_VF_POWER_STATE 若要更改电源状态的指定 PCI Express (PCIe) 虚拟函数 (VF) 网络适配器上。
ms.assetid: 9723518E-2312-48F9-820A-19F5567A33DB
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_SET_VF_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6f8d73086a5f7ba2e10d92cd23e92a548c71fec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351332"
---
# <a name="oidsriovsetvfpowerstate"></a>OID\_SRIOV\_SET\_VF\_POWER\_STATE


基础驱动程序将发出对象标识符 (OID) 组请求的 OID\_SRIOV\_设置\_VF\_POWER\_状态上更改电源状态的指定 PCI Express (PCIe) 虚拟函数 (VF)网络适配器。 由于更改的电源状态是一项特权的操作，基础驱动程序微型端口驱动程序的 PCIe 物理函数 (PF) 网络适配器上发出此 OID 集请求。 PF 微型端口驱动程序然后 VF 上设置指定的电源状态。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_SRIOV\_设置\_VF\_POWER\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451683)结构。

<a name="remarks"></a>备注
-------

当此 OID 集请求发出 PF 微型端口驱动程序，则它必须遵循以下准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_设置\_VF\_POWER\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451683)结构，具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果指定的 VF 不处于已分配状态，该驱动程序必须故障 OID 请求。

-   电源状态操作只会影响指定的 VF。 该操作必须不影响其他 VFs 或同一个网络适配器上的 PF。

有关详细信息，请参阅[设置电源状态的虚拟函数](https://msdn.microsoft.com/library/windows/hardware/hh440230)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序返回以下状态代码之一 OID 设置请求的 OID\_SRIOV\_设置\_VF\_POWER\_状态。

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
<td><p>PF 微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451683" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451683)"> <strong>NDIS_SRIOV_SET_VF_POWER_STATE_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 PF 微型端口驱动程序必须设置<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_SET\_VF\_POWER\_STATE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451683)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




