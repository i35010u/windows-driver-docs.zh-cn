---
title: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS （0xDD）
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS 是包含用于 IPv6 的 Rx 校验和卸载的 TLV。
ms.assetid: F647B2B6-F535-4AE2-B7A9-DF08AADB2A95
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS （0xDD）从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7eeb6416eeda52541839d8cf4aad98d8ee1b853f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841641"
---
# <a name="wdi_tlv_checksum_offload_v6_rx_parameters-0xdd"></a>WDI\_TLV\_校验和\_卸载\_V6\_RX\_参数（0xDD）


WDI\_TLV\_校验和\_卸载\_V6\_RX\_参数是包含用于 IPv6 的 Rx 校验和卸载的 TLV。

功能值以[**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)的形式报告。 使用 NDIS\_卸载\_不\_受支持，并且通过[OID\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)时，支持 NDIS\_卸载\_。

## <a name="tlv-type"></a>TLV 类型


0xDD

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
<td>指定是否支持卸载具有 IP 扩展标头的数据包的校验和。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否支持卸载带有 TCP 选项的校验和。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定是否启用 TCP 校验和卸载。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否启用 UDP 卸载。</td>
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

 

 




