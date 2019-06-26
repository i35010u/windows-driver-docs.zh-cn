---
title: WDI_TLV_LSO_V1_CAPABILITIES (0xCC)
description: WDI_TLV_LSO_V1_CAPABILITIES 是包含大量发送卸载 V1 功能 TLV。
ms.assetid: 22C5778A-F551-4931-A19C-7AA399221B3D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LSO_V1_CAPABILITIES (0xCC) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4f9a814f2db63dd713f8f50dd8750bf95a79e0eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354466"
---
# <a name="wditlvlsov1capabilities-0xcc"></a>WDI\_TLV\_LSO\_V1\_功能 (0xCC)


WDI\_TLV\_LSO\_V1\_功能是包含大量发送卸载 V1 功能 TLV。

将报告功能值，如中所述[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)。 使用 NDIS\_卸载\_不\_支持和 NDIS\_卸载\_时，该值指示通过功能支持[OID\_WDI\_GET\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)。

## <a name="tlv-type"></a>TLV 类型


0xCC

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
<td>封装类型中。 有效值包括：
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
<td>必须是整除之前传输大型 TCP 数据包的段的最小数目可卸载它到分段的硬件。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定支持此卸载 TCP 选项。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定支持此卸载 IP 选项。</td>
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

 

 




