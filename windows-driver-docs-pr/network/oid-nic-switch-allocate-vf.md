---
title: OID_NIC_SWITCH_ALLOCATE_VF
description: 过量驱动程序) 方法请求 (OID 发出对象标识符，OID_NIC_SWITCH_ALLOCATE_VF 为 PCI Express (PCIe) 虚拟函数 (VF) 分配资源。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_ALLOCATE_VF 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6c77a5e045605503ae7b1bf82b85513ff7f0ea0f
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248575"
---
# <a name="oid_nic_switch_allocate_vf"></a>OID \_ NIC \_ 交换机 \_ 分配 \_ VF


过量驱动程序发出对象标识符 (oid) 方法请求 OID \_ NIC \_ 交换机 \_ 分配 \_ VF，为 PCI Express (PCIe) 虚函数 (VF) 分配资源。 VF 在支持单个根 i/o 虚拟化 (SR-IOV) 接口的网络适配器上公开。

过量驱动程序将此 OID 方法请求发送到网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。

<a name="remarks"></a>备注
-------

当驱动程序处理 OID \_ NIC \_ 交换机 \_ 分配 VF 的对象标识符 (oid) 方法请求时，PF 微型端口驱动程序为 VF 分配软件资源 \_ 。 即使已为 VF 分配硬件资源，也会将其视为 nonoperational，直到 PF 微端口驱动程序成功完成 OID \_ NIC \_ 交换机 \_ 分配 \_ VF。

有关如何分配 VF 资源的详细信息，请参阅为 [虚拟函数分配资源](./allocating-resources-for-a-virtual-function.md)。

**注意**  在过量驱动程序为 VF 请求分配资源后，该驱动程序是唯一可请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid [ \_ NIC \_ 交换机 \_ 自由 \_ vf](oid-nic-switch-free-vf.md) 的 OID 设置请求，以释放 vf 资源。 在停止过量驱动程序之前，必须释放由驱动程序的 OID \_ NIC \_ 交换机 \_ 分配 \_ vf 请求分配的每个 VF 的资源。

 

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ NIC \_ 交换机 \_ 分配 VF 的 oid 方法请求，PF 微型端口驱动程序返回以下状态代码之一 \_ 。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>) 。 PF 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ 成为 \_ RID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_make_rid)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)

[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[OID \_ NIC \_ 交换机 \_ 免费 \_ VF](oid-nic-switch-free-vf.md)

