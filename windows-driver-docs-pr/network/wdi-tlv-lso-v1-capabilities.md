---
title: 'WDI_TLV_LSO_V1_CAPABILITIES (0xCC) '
description: WDI_TLV_LSO_V1_CAPABILITIES 是包含大量发送卸载 V1 功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LSO_V1_CAPABILITIES (0xCC) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 68e987d94aa0dedfe2eb8e2608b267d7e1327fc5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818277"
---
# <a name="wdi_tlv_lso_v1_capabilities-0xcc"></a>WDI \_ TLV \_ LSO \_ V1 \_ 功能 (0xCC) 


WDI \_ tlv \_ LSO \_ v1 \_ 功能是包含大量 Send 卸载 V1 功能的 tlv。

将按 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)中所述报告功能值。 使用 \_ \_ 不 \_ 受支持的 ndis 卸载，并 \_ \_ 在通过 [OID \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)指示功能时支持 ndis 卸载。

## <a name="tlv-type"></a>TLV 类型


0xCC

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

 

