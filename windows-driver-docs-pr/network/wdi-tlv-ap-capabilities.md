---
title: WDI_TLV_AP_CAPABILITIES
description: WDI_TLV_AP_CAPABILITIES 是包含访问点功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a911b51d12961dffa831347d375b5c77cda0e37c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823799"
---
# <a name="wdi_tlv_ap_capabilities"></a>WDI \_ TLV \_ AP \_ 功能


WDI \_ tlv \_ AP \_ 功能是包含访问点功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x16

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
<td>扫描 SSID 列表大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>所需的 SSID 列表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>隐私例外列表大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>关联表的大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>键映射表大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>默认的键表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP 密钥值的最大长度。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定 AP 是否支持雷达检测。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
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

 

 




