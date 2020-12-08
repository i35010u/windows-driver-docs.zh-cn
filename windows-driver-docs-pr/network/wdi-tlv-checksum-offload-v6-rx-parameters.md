---
title: 'WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0xDD) '
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS 是包含用于 IPv6 的 Rx 校验和卸载的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHECKSUM_OFFLOAD_V6_RX_PARAMETERS (0xDD) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 80231e23b976fae82acdd07d9b72a67f98297592
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814899"
---
# <a name="wdi_tlv_checksum_offload_v6_rx_parameters-0xdd"></a>WDI \_ TLV \_ 校验和 \_ 卸载 \_ V6 \_ RX \_ 参数 (0xDD) 


WDI \_ tlv \_ 校验和 \_ 卸载 \_ V6 \_ RX \_ 参数是包含用于 IPv6 的 RX 校验和卸载的 tlv。

将按 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)中所述报告功能值。 使用 \_ \_ 不 \_ 受支持的 ndis 卸载，并 \_ \_ 在通过 [OID \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)指示功能时支持 ndis 卸载。

## <a name="tlv-type"></a>TLV 类型


0xDD

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>封装类型。 有效值是：
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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

