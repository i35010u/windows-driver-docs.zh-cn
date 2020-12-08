---
title: WDI_TLV_P2P_ADVERTISED_SERVICES
description: WDI_TLV_P2P_ADVERTISED_SERVICES 是包含播发服务列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e8d160d490961e1024eaaf6a36049827acd53a73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823793"
---
# <a name="wdi_tlv_p2p_advertised_services"></a>WDI \_ TLV \_ P2P \_ 播发 \_ 服务


WDI \_ tlv \_ P2P \_ 播发 \_ 服务是包含播发服务列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xEF

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td>播发服务列表。</td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-advertised-prefix-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-prefix-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>从播发服务列表派生的播发前缀列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-asp2-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-asp2-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
<p>播发的 ASP2 服务的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-service-update-indicator.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR&lt;/strong&gt;](wdi-tlv-p2p-service-update-indicator.md)"><strong>WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR</strong></a></p></td>
<td></td>
<td></td>
<td><p>如果驱动程序支持响应服务信息发现 ANQP 请求，则包含在 ANQP 响应中的服务更新指示器。</p></td>
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

 

 




