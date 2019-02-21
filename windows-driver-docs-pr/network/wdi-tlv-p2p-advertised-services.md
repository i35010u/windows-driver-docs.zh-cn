---
title: WDI_TLV_P2P_ADVERTISED_SERVICES
description: WDI_TLV_P2P_ADVERTISED_SERVICES 是 TLV 包含公布的服务的列表。
ms.assetid: C210DDF3-0349-4108-82EC-1823F562E5D7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c684ff1415f0391ad6f359638839011a74973128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524434"
---
# <a name="wditlvp2padvertisedservices"></a>WDI\_TLV\_P2P\_ADVERTISED\_SERVICES


WDI\_TLV\_P2P\_播发\_服务是包含一系列公布的服务 TLV。

## <a name="tlv-type"></a>TLV 类型


0xEF

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

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
<th>在任务栏的搜索框中键入</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td>公布的服务的列表。</td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-advertised-prefix-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-advertised-prefix-entry.md)"><strong>WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>派生自的公布的服务列表的播发前缀的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-p2p-asp2-advertised-service-entry.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](wdi-tlv-p2p-asp2-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
<p>播发 ASP2 服务的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdi-tlv-p2p-service-update-indicator.md" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR&lt;/strong&gt;](wdi-tlv-p2p-service-update-indicator.md)"><strong>WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR</strong></a></p></td>
<td></td>
<td></td>
<td><p>要包括在 ANQP 响应中，如果该驱动程序支持对服务的信息发现 ANQP 请求的响应的服务更新指示器。</p></td>
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

 

 




