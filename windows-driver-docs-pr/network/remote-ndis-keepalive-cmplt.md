---
title: REMOTE_NDIS_KEEPALIVE_CMPLT
description: 远程 NDIS 设备将通过发送回 REMOTE_NDIS_KEEPALIVE_CMPLT 响应消息来响应来自主机的 REMOTE_NDIS_KEEPALIVE_MSG 消息。
ms.assetid: c090b781-73f1-4a7a-a0a2-60af366daa77
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0c2b82418abf205c84103d74dc4abb2a18a8c4
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969404"
---
# <a name="remote_ndis_keepalive_cmplt"></a>远程 \_ NDIS \_ KEEPALIVE \_ CMPLT


远程 ndis 设备将通过回发远程 ndis keepalive CMPLT 响应消息，来响应来自主机的 [**远程 \_ ndis \_ keepalive \_ **](remote-ndis-keepalive-msg.md) 消息消息 \_ \_ \_ 。 如果返回的状态不是 "RNDIS" \_ \_ ，则主机将发送 [**远程 \_ NDIS \_ reset \_ MSG**](remote-ndis-reset-msg.md) 以重置设备。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Offset</th>
<th>大小</th>
<th>字段</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>4</p></td>
<td><p>MessageType</p></td>
<td><p>指定要发送的消息的类型。 设置为0x80000008。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>MessageLength</p></td>
<td><p>指定从消息开头开始的此消息的总长度（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>4</p></td>
<td><p>RequestId</p></td>
<td><p>指定远程 NDIS 消息 ID 值。 此值用于匹配主机发送的包含设备响应的消息。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>状态</p></td>
<td><p>指定设备的当前状态。 如果返回的 <em>状态</em> 不是 RNDIS_STATUS_SUCCESS，则主机将发送 <a href="remote-ndis-reset-msg.md" data-raw-source="[&lt;strong&gt;REMOTE_NDIS_RESET_MSG&lt;/strong&gt;](remote-ndis-reset-msg.md)"><strong>REMOTE_NDIS_RESET_MSG</strong></a> 消息来重置设备。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

如果设备实现了发送 [**远程 \_ ndis \_ keepalive \_ 消息**](remote-ndis-keepalive-msg.md)的选项，则主机将 \_ \_ \_ 通过控制通道使用远程 ndis keepalive CMPLT 进行响应。

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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




