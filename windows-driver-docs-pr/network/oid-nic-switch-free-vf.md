---
title: OID_NIC_SWITCH_FREE_VF
description: 基础驱动程序发出的对象标识符 (OID) 组请求的 OID_NIC_SWITCH_FREE_VF 释放资源的网络适配器的 PCI Express (PCIe) 虚拟函数 (VF)。基础驱动程序此 OID 集向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 集请求是必需的 PF 微型端口驱动程序支持单个根 I/O 虚拟化 (SR-IOV) 接口。
ms.assetid: B1A72D34-286A-4A70-8BE3-F21324B92187
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_FREE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5469c272ed6c52721e0c2a3e374b5a8811f341c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350974"
---
# <a name="oidnicswitchfreevf"></a>OID\_NIC\_交换机\_免费\_VF


基础驱动程序将发出对象标识符 (OID) 组请求的 OID\_NIC\_交换机\_免费\_VF 释放资源的网络适配器的 PCI Express (PCIe) 虚拟函数 (VF)。

基础驱动程序此 OID 集向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 集请求是必需的 PF 微型端口驱动程序支持单个根 I/O 虚拟化 (SR-IOV) 接口。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_免费\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451579)结构。

基础驱动程序指定的标识符的取景器通过释放**VFId**此结构的成员。 该驱动程序从较早的 OID 方法请求获取此标识符[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

<a name="remarks"></a>备注
-------

基础驱动程序发出 OID 集请求的 OID\_NIC\_交换机\_免费\_VF 为 VF 释放资源。 这些资源之前通过 OID 方法请求的分配[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

有关如何对可用的取景器资源的详细信息，请参阅[为虚拟函数释放资源](https://msdn.microsoft.com/library/windows/hardware/hh439570)。

**请注意**  后基础驱动程序请求 VF 的资源分配时，该驱动程序是可以请求的同一 VF 释放资源的唯一组件。 基础驱动程序必须发出 OID 集请求的 OID\_NIC\_交换机\_免费\_VF 来释放 VF 资源。 可以暂停基础驱动程序之前，它必须释放资源的已分配的驱动程序的每个 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)请求。

 

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数将返回以下值之一用于此请求：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>微型端口驱动程序已成功完成请求。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>微型端口驱动程序将以异步方式完成的请求。 微型端口驱动程序已完成所有处理后，它必须请求成功通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>函数，传递<strong>NDIS_STATUS_SUCCESS</strong>对于<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口驱动程序正在重置。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，名为 NDIS <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>函数。</p></td>
</tr>
</tbody>
</table>

 

NDIS 返回此请求的以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p>一个或多个的成员<a href="https://msdn.microsoft.com/library/windows/hardware/hh451579" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_FREE_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451579)"> <strong>NDIS_NIC_SWITCH_FREE_VF_PARAMETERS</strong> </a>结构具有无效值。 例如， <strong>VFId</strong>成员可能指定的 VF 或者尚未分配或者具有尚未删除的 VPorts。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区因过小。 NDIS 集<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
[**NDIS\_NIC\_SWITCH\_FREE\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451579)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_交换机\_删除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_交换机\_删除\_开关](oid-nic-switch-delete-switch.md)

 

 




