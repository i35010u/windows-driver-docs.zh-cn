---
title: OID_NIC_SWITCH_DELETE_VPORT
description: 基础驱动程序发出的对象标识符 (OID) 组请求的 OID_NIC_SWITCH_DELETE_VPORT 若要删除非默认网络适配器的 NIC 交换机先前创建的虚拟端口 (VPort)。
ms.assetid: D762035C-33AC-4579-8EA0-6A422AE4CA76
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_DELETE_VPORT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 08694aa633a52fa0bf415ece1bf4bd01800354a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523496"
---
# <a name="oidnicswitchdeletevport"></a>OID\_NIC\_交换机\_删除\_VPORT


基础驱动程序将发出对象标识符 (OID) 组请求的 OID\_NIC\_交换机\_删除\_VPORT 删除先前创建的网络适配器的 NIC 的非默认虚拟端口 (VPort)切换。 基础驱动程序可以删除它以前创建了仅通过发出的 OID 方法请求 VPort [OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)。

基础驱动程序此 OID 集向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 集请求是必需的 PF 微型端口驱动程序支持单个根 I/O 虚拟化 (SR-IOV) 接口。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_删除\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451577)结构。

<a name="remarks"></a>备注
-------

基础驱动程序，如协议或筛选器驱动程序，只能删除非默认 VPort 以前创建了它。 基础驱动程序通过发出的 OID 方法请求创建 VPort [OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)。

当 PF 微型端口驱动程序收到的 OID OID 请求\_NIC\_交换机\_删除\_VPORT，驱动程序必须释放已分配给指定 VPort 的硬件和软件资源。

有关详细信息，请参阅[删除虚拟端口](https://msdn.microsoft.com/library/windows/hardware/hh439418)。

**请注意**  非默认，可以通过 OID 的 OID 请求显式删除 VPorts\_NIC\_交换机\_删除\_VPORT。 PF 微型端口驱动程序删除默认 NIC 交换机时，默认 VPort 是隐式删除。 有关详细信息，请参阅[删除 NIC 交换机](https://msdn.microsoft.com/library/windows/hardware/hh439415)。

 

### <a name="return-status-codes"></a>返回状态代码

PF 微型端口驱动程序返回以下状态代码之一 OID 设置请求的 OID\_NIC\_交换机\_删除\_VPORT。

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
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451577" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451577)"> <strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451577" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451577)"><strong>NDIS_NIC_SWITCH_DELETE_VPORT_PARAMETERS</strong></a>)。 PF 微型端口驱动程序必须设置<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_SWITCH\_DELETE\_VPORT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451577)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_删除\_开关](oid-nic-switch-delete-switch.md)

 

 




