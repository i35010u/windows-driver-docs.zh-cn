---
title: OID_SRIOV_RESET_VF
description: 过量驱动程序问题的对象标识符 (OID) 设置的 OID_SRIOV_RESET_VF 的请求以重置指定 PCI Express (PCIe) 虚拟函数 (VF) 上支持单根 I/O 虚拟化的网络适配器。
ms.assetid: 7D5EB64B-3345-478A-8D42-192939C0B9C2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_RESET_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1484aa08143befd9544f0237b73c08806addb440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540559"
---
# <a name="oidsriovresetvf"></a>OID\_SRIOV\_RESET\_VF


过量驱动程序问题的对象标识符 (OID) 会将请求设置的 OID\_SRIOV\_重置\_VF 重置指定 PCI Express (PCIe) 虚拟函数 (VF) 支持单根 I/O 虚拟化的网络适配器上。 基础驱动程序微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的网络适配器向颁发此 OID 集请求。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_SRIOV\_重置\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451682)结构。 基础驱动程序指定要重置通过 VF 的标识符**VFId**此结构的成员。

<a name="remarks"></a>备注
-------

VF 可以重置通过 PCI Express (PCIe) 函数级别重置 (FLR)。 由于 FLR 请求是一项特权的操作，只能由管理操作系统的 HYPER-V 父分区中运行的 PF 微型端口驱动程序执行。 在管理操作系统中运行的基础驱动程序通知 FLR 请求和问题的 OID 设置请求的 OID\_SRIOV\_重置\_VF 到 PF 微型端口驱动程序。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_重置\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451682)结构，具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   重置操作只会影响指定的 VF。 该操作必须不影响其他 VFs 或同一个网络适配器上的 PF。

有关详细信息，请参阅[重置虚拟函数](https://msdn.microsoft.com/library/windows/hardware/hh440219)。

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的集请求的以下状态代码\_SRIOV\_重置\_VF。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451682" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_RESET_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451682)"> <strong>NDIS_SRIOV_RESET_VF_PARAMETERS</strong> </a>结构具有无效值。</p></td>
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
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_RESET\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451682)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




