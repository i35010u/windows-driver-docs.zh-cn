---
title: OID_802_3_DELETE_MULTICAST_ADDRESS
description: 作为 set 请求，NDIS 和基础协议驱动程序使用 OID_802_3_DELETE_MULTICAST_ADDRESS OID 从微型端口适配器多路广播的地址列表中删除以前添加的多播的地址。
ms.assetid: 5efaa724-80b4-4721-a1b0-8ba67c03bb32
ms.date: 08/08/2017
keywords: -OID_802_3_DELETE_MULTICAST_ADDRESS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1edd7f5dfe57c943a05daf4277b00544eb6baf87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541808"
---
# <a name="oid8023deletemulticastaddress"></a>OID\_802\_3\_删除\_多播\_地址


为 set 请求，NDIS 和基础协议驱动程序使用 OID\_802\_3\_删除\_多播\_地址 OID 的多播的地址列表中删除以前添加的多播的地址微型端口适配器。 多播的地址是 6 个字节的数组。 正在删除地址禁用该地址，以便它不再接收多路广播的数据包。

**版本信息**

<a href="" id="windows-vista"></a>Windows Vista  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含要从删除的 6 个字节地址多播的地址列表。

OID\_802\_3\_删除\_多播\_地址 OID 请求可以删除只能有一个地址。 若要删除多个地址，协议驱动程序必须发出多个 OID\_802\_3\_删除\_多播\_地址 OID 请求。

NDIS 微型端口驱动程序不直接接收此 OID 请求。 相反，NDIS 合并的每个序列[OID\_802\_3\_添加\_多播\_地址](oid-802-3-add-multicast-address.md)和 OID\_802\_3\_删除\_多播\_地址 OID 请求到单个[OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)OID 请求。

若要替换或删除多路广播的完整列表，协议驱动程序可以使用[OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)OID 请求。

若要将地址添加到列表中，协议驱动程序可以使用[OID\_802\_3\_添加\_多播\_地址](oid-802-3-add-multicast-address.md)OID 请求。

基础协议驱动程序可以添加给定的多播的地址多次通过发送多个[OID\_802\_3\_添加\_多播\_地址](oid-802-3-add-multicast-address.md)OID 请求. 如果 NDIS 成功为给定的多播地址的第一个添加请求，NDIS 将成功执行所有后续添加该地址的请求。 若要删除已超过一次添加一个多播的地址，基础驱动程序必须删除的地址的地址，添加相同次数。

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

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_802\_3\_ADD\_MULTICAST\_ADDRESS](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_MAXIMUM\_LIST\_SIZE](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_MULTICAST\_LIST](oid-802-3-multicast-list.md)

 

 




