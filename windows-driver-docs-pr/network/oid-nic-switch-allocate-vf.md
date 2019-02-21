---
title: OID_NIC_SWITCH_ALLOCATE_VF
description: 基础驱动程序发出的对象标识符 (OID) 方法请求的 OID_NIC_SWITCH_ALLOCATE_VF 分配为 PCI Express (PCIe) 虚拟函数 (VF) 的资源。
ms.assetid: CB88CE0C-705F-406B-90FE-FB206D6F4864
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ALLOCATE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a0cf4c274579407ab4034141e93e7ea61d659720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519106"
---
# <a name="oidnicswitchallocatevf"></a>OID\_NIC\_交换机\_分配\_VF


基础驱动程序发出的 OID 的对象标识符 (OID) 方法请求\_NIC\_交换机\_分配\_VF 分配为 PCI Express (PCIe) 虚拟函数 (VF) 的资源。 VF 公开支持的单个根 I/O 虚拟化 (SR-IOV) 接口的网络适配器。

基础驱动程序此 OID 方法向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

<a name="remarks"></a>备注
-------

PF 微型端口驱动程序分配 VF 软件资源时，驱动程序处理的 OID 的对象标识符 (OID) 方法请求\_NIC\_交换机\_分配\_VF。 即使已为 VF 分配硬件资源，它被视为可不再运行，直到 PF 微型端口驱动程序已成功完成 OID\_NIC\_交换机\_分配\_VF。

有关如何分配 VF 资源的详细信息，请参阅[虚函数的分配资源](https://msdn.microsoft.com/library/windows/hardware/hh439285)。

**请注意**  基础驱动程序请求 VF 的资源分配该驱动程序后，可以请求的同一 VF 释放资源的唯一组件。 基础驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](oid-nic-switch-free-vf.md)来释放 VF 资源。 可以暂停基础驱动程序之前，它必须释放资源，为每个已分配的驱动程序的 OID 的 VF\_NIC\_交换机\_分配\_VF 请求。

 

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_NIC\_交换机\_分配\_VF。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>)。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_使\_RID**](https://msdn.microsoft.com/library/windows/hardware/hh451557)

[OID\_NIC\_SWITCH\_CREATE\_SWITCH](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593)

[OID\_NIC\_SWITCH\_FREE\_VF](oid-nic-switch-free-vf.md)

 

 




