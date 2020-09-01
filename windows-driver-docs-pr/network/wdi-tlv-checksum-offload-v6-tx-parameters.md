---
title: 'WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS (0xDC) '
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS 是包含适用于 IPv6 的 Tx 校验和卸载的 TLV。
ms.assetid: F0340707-4E81-4E66-AF0E-A2918F4F5C7A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS (0xDC) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eb1b0a146c8938509cb2d7c286717ed1590fa9c9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208512"
---
# <a name="wdi_tlv_checksum_offload_v6_tx_parameters-0xdc"></a>WDI \_ TLV \_ 校验和 \_ 卸载 \_ V6 \_ TX \_ 参数 (0xDC) 


WDI \_ tlv \_ 校验和 \_ 卸载 \_ V6 \_ TX \_ 参数是一个 TLV，其中包含适用于 IPv6 的 TX 校验和卸载。

将按 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)中所述报告功能值。 使用 \_ \_ 不 \_ 受支持的 ndis 卸载，并 \_ \_ 在通过 [OID \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)指示功能时支持 ndis 卸载。

## <a name="tlv-type"></a>TLV 类型


0xDC

## <a name="length"></a>Length


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
<th>说明</th>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

