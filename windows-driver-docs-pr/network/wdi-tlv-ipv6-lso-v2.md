---
title: WDI_TLV_IPV6_LSO_V2 (0xD4)
description: WDI_TLV_IPV6_LSO_V2 是包含大量发送卸载 V2 参数对 IPv6 TLV。
ms.assetid: 898257D1-405A-46A3-AE63-26DFA8C1FAAC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IPV6_LSO_V2 (0xD4) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb7912d8cb30bd2c25ad53e8c6adb488e65f2e7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390962"
---
# <a name="wditlvipv6lsov2-0xd4"></a>WDI\_TLV\_IPV6\_LSO\_V2 (0xD4)


WDI\_TLV\_IPV6\_LSO\_V2 是包含大量发送卸载 V2 参数对 IPv6 TLV。

将报告功能值，如中所述[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)。 使用 NDIS\_卸载\_不\_支持和 NDIS\_卸载\_时，该值指示通过功能支持[OID\_WDI\_GET\_适配器\_功能](https://msdn.microsoft.com/library/windows/hardware/dn925838)。

## <a name="tlv-type"></a>TLV 类型


0xD4

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
<tr class="even">
<td>UINT32</td>
<td>指定是否支持卸载 IP 扩展标头的数据包的校验和。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否支持使用 TCP 选项的校验和卸载。</td>
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

 

 




