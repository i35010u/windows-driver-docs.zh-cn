---
title: OID_SRIOV_PF_LUID
description: 过量驱动程序发出 (OID 的对象标识符) 查询请求，OID_SRIOV_PF_LUID 接收本地唯一标识符 (LUID) 关联到网络适配器的 PCI Express (PCIe) 物理函数 (。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_PF_LUID 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 830a748c834e15cae113e080530095a36f21e2e7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248627"
---
# <a name="oid_sriov_pf_luid"></a>OID \_ SRIOV \_ PF \_ LUID


过量驱动程序发出 (oid 的对象标识符) 查询 OID 请求， \_ \_ \_ 以接收与 PCI Express (PCIe 关联的本地唯一标识符 (LUID) 与网络适配器) PF (。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ SRIOV \_ PF \_ LUID \_ INFO**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_pf_luid_info)结构的指针。

<a name="remarks"></a>备注
-------

在 NDIS 为 pf 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数之前，NDIS 为 PF 生成 LUID。 在 NDIS 调用驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数之前，此 LUID 是有效的。

**注意** **Luid** 成员的值不同于 [**NDIS \_ 微型端口 \_ 初始 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的 **NetLuid** 成员。 通过 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的 *MiniportInitParameters* 参数将此结构传递给微型端口驱动程序。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ \_ 对微型端口驱动程序执行 oid SRIOV PF LUID 请求的 oid 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ SRIOV \_ PF \_ LUID 请求时，它将返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
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
[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ SRIOV \_ PF \_ LUID \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_pf_luid_info)

