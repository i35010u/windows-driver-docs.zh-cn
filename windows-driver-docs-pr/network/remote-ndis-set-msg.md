---
title: REMOTE_NDIS_SET_MSG
description: 当需要在设备上设置某些操作参数的值时，会将此消息从主机发送到远程 NDIS 设备。
ms.assetid: d39032e2-e3a5-415f-8bd6-b60b9049ce33
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 251a486515dae67996e589588318789e0da69fc3
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968726"
---
# <a name="remote_ndis_set_msg"></a>远程 \_ NDIS \_ 设置 \_ 消息


当需要在设备上设置某些操作参数的值时，会将此消息从主机发送到远程 NDIS 设备。 要设置的特定参数通过对象标识符 (OID) 来标识，并且要将其设置为的值包含在与消息一起发送的信息缓冲区中。 当 \_ \_ \_ 设备处于远程 ndis 初始化的状态时，主机可能会通过控制通道将远程 NDIS SET MSG 发送到设备。 远程 NDIS 设备将通过 \_ 向主机发送远程 ndis 集 CMPLT 来响应此消息 \_ \_ 。

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
<td><p>指定要发送的消息的类型。 设置为0x00000005。</p></td>
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
<td><p>Oid</p></td>
<td><p>指定用于标识要设置的参数的 NDIS OID。</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>4</p></td>
<td><p>InformationBufferLength</p></td>
<td><p>指定请求的输入数据的长度（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td><p>20</p></td>
<td><p>4</p></td>
<td><p>InformationBufferOffset</p></td>
<td><p>指定请求的输入数据位于 <em>RequestId</em> 字段开头的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td><p>24</p></td>
<td><p>4</p></td>
<td><p>DeviceVcHandle</p></td>
<td><p>为面向连接的设备保留。 设置为零。</p></td>
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
<td><p>在 Microsoft Windows XP 和更高版本的 Windows 操作系统中可用。 在 Windows 2000 中也可以作为可再发行二进制文件。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Rndis (包含 Rndis) </td>
</tr>
</tbody>
</table>

 

 




