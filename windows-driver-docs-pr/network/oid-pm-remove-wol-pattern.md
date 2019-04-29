---
title: OID_PM_REMOVE_WOL_PATTERN
description: 作为一组 NDIS 和协议驱动程序使用 OID_PM_REMOVE_WOL_PATTERN OID 删除网络适配器从电源管理唤醒 LAN (WOL) 模式。
ms.assetid: fdaa2646-6f41-4f51-9c27-6194270f26ed
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_REMOVE_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b0bea9946e514bb9d7fea65017ff5b953f7e1e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359162"
---
# <a name="oidpmremovewolpattern"></a>OID\_PM\_删除\_WOL\_模式


作为一组 NDIS 和协议驱动程序使用 OID\_PM\_删除\_WOL\_模式 OID，若要删除的网络适配器从电源管理唤醒 LAN (WOL) 模式。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向 ULONG 模式标识符。

<a name="remarks"></a>备注
-------

NDIS 和协议驱动程序使用 OID\_PM\_删除\_WOL\_从基础的网络适配器中删除唤醒 LAN (WOL) 模式的模式。

**数据。设置\_INFORMATION.InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构必须指向以前添加的 WOL 模式标识符的 ULONG 值。 NDIS 中设置此模式标识符**PatternId**的成员[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构时 NDIS发送在先前[OID\_PM\_添加\_WOL\_模式](oid-pm-add-wol-pattern.md)OID 为基础的网络适配器的请求。

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
<td><p>微型端口驱动程序的 NDIS 版本小于 NDIS 6.20。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p>OID 请求中的模式标识符是无效的。</p></td>
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
<td><p>支持 NDIS 6.20 及更高版本。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_WOL\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[OID\_PM\_ADD\_WOL\_PATTERN](oid-pm-add-wol-pattern.md)

[**NDIS\_状态\_PM\_WOL\_模式\_已拒绝**](https://msdn.microsoft.com/library/windows/hardware/ff567414)

 

 




