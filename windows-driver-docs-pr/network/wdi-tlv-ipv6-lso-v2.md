---
title: WDI_TLV_IPV6_LSO_V2 (0xD4)
description: WDI_TLV_IPV6_LSO_V2 是一个 TLV，其中包含 IPv6 的大型发送卸载 V2 参数。
ms.assetid: 898257D1-405A-46A3-AE63-26DFA8C1FAAC
ms.date: 07/18/2017
keywords:
- WDI_TLV_IPV6_LSO_V2 （0xD4）从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ec794d7cdd2909f8b662495f6dba6eb3bdbdcb99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842464"
---
# <a name="wdi_tlv_ipv6_lso_v2-0xd4"></a>WDI\_TLV\_IPV6\_LSO\_V2 （0xD4）


WDI\_TLV\_IPV6\_LSO\_V2 是包含 IPv6 的大型发送卸载 V2 参数的 TLV。

功能值以[**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)的形式报告。 使用 NDIS\_卸载\_不\_受支持，并且通过[OID\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)时，支持 NDIS\_卸载\_。

## <a name="tlv-type"></a>TLV 类型


0xD4

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

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
<td>最大卸载大小。 由每个数据包的 TCP 用户数据的最大字节数指定。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最小段计数。 由分段后应出现的段数的最小数目指定。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定是否支持卸载具有 IP 扩展标头的数据包的校验和。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否支持卸载带有 TCP 选项的校验和。</td>
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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




