---
title: WDI_TLV_LSO_V1_CAPABILITIES （0xCC）
description: WDI_TLV_LSO_V1_CAPABILITIES 是包含大量 Send 卸载 V1 功能的 TLV。
ms.assetid: 22C5778A-F551-4931-A19C-7AA399221B3D
ms.date: 07/18/2017
keywords:
- WDI_TLV_LSO_V1_CAPABILITIES （0xCC）从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d4724e07e305fb4d370d437948876992afabc2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842463"
---
# <a name="wdi_tlv_lso_v1_capabilities-0xcc"></a>WDI\_TLV\_LSO\_V1\_功能（0xCC）


WDI\_TLV\_LSO\_V1\_功能是包含大型发送卸载 V1 功能的 TLV。

功能值以[**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)的形式报告。 使用 NDIS\_卸载\_不\_受支持，并且通过[OID\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)时，支持 NDIS\_卸载\_。

## <a name="tlv-type"></a>TLV 类型


0xCC

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
<td>大型 TCP 数据包在传输之前必须可以被整除的最小段数，以便将其卸载到硬件进行分段。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定此卸载是否支持 TCP 选项。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定此卸载是否支持 IP 选项。</td>
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

 

 




