---
title: WDI_TLV_IPV4_LSO_V2 (0xD3)
description: WDI_TLV_IPV4_LSO_V2 是包含大量发送卸载 V2 参数的 IPv4 TLV。
ms.assetid: 912D5F1B-260F-43B3-93F6-3C38E9D7F1E5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IPV4_LSO_V2 (0xD3) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 67ec713d8842231a1be77c7f3d2d7faa531e4064
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363025"
---
# <a name="wditlvipv4lsov2-0xd3"></a>WDI\_TLV\_IPV4\_LSO\_V2 (0xD3)


WDI\_TLV\_IPV4\_LSO\_V2 是包含大量发送卸载 V2 参数的 IPv4 TLV。

## <a name="tlv-type"></a>TLV 类型


0xD3

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>封装类型。 有效值包括：
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>卸载最大大小。 指定的最大的每个数据包的 TCP 用户数据的字节数。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最小的段计数。 指定应将分段后出现的段的最小数目。</td>
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
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




