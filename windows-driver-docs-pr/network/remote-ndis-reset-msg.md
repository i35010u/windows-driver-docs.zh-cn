---
title: REMOTE_NDIS_RESET_MSG
description: 此消息将从主机发送到远程 NDIS 设备，以重置设备并返回状态。
ms.assetid: b5938b0d-75bf-497f-afeb-9950b383af5e
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfa815c5df7846e6b85845606f424fd69c58f194
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969590"
---
# <a name="remote_ndis_reset_msg"></a>远程 \_ NDIS \_ 重置 \_ 消息


此消息将从主机发送到远程 NDIS 设备，以重置设备并返回状态。 当 \_ 设备处于远程 ndis 初始化的状态时，主机可能会 \_ 通过控制通道向设备发送远程 ndis 重置 \_ 消息。 远程 NDIS 设备将通过 \_ 向主机发送远程 ndis \_ 重置 CMPLT 来响应此消息 \_ 。

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
<td><p>指定要发送的消息的类型。 设置为0x00000006。</p></td>
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
<td><p>预留</p></td>
<td><p>保留。 设置为零。</p></td>
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

 

 




