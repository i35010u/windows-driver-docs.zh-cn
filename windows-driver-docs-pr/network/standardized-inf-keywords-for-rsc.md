---
title: RSC 的标准化 INF 关键字
description: RSC 的标准化 INF 关键字
keywords:
- 接收方合并 WDK 网络，标准化 INF 关键字
- RSC WDK 网络，标准化 INF 关键字
- 标准化 INF 关键字 WDK RSC
- INF 项 WDK RSC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f32ce78f3e2d19e6ef80101146a0c7275e3da29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787167"
---
# <a name="standardized-inf-keywords-for-rsc"></a>RSC 的标准化 INF 关键字





在 Windows 8、Windows Server 2012 和更高版本中，接收段合并 (RSC) 接口支持显示在注册表中并在 INF 文件中指定的 [标准 inf 关键字](standardized-inf-keywords-for-network-devices.md) 。

以下列表显示了适用于 RSC 的枚举 [标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md) ：

<a href="" id="-rscipv4"></a>**\*RscIPv4**  
为 IPv4 数据报版本启用或禁用 RSC 支持。

<a href="" id="---------rscipv6"></a>**\* RscIPv6**  
为 IPv6 数据报版本启用或禁用 RSC 支持。

枚举标准化 INF 关键字具有以下属性：

<a href="" id="subkeyname"></a>**SubkeyName**  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>**ParamDesc**  
与 **SubkeyName** 关联的显示文本。

<a href="" id="value"></a>**负值**  
与列表中的每个选项关联的枚举整数值。 此值存储在 NDI \\ params \\ *SubkeyName* \\ *值* 中。

<a href="" id="enumdesc"></a>**EnumDesc**  
与菜单中显示的每个值相关联的显示文本。

<a href="" id="default"></a>**缺省值**  
菜单的默认值。

下表描述了 RSC 枚举关键字的可能 INF 条目。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">“值”</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RscIPv4</strong></p></td>
<td align="left"><p> (IPv4 接收段合并) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>RscIPv6</strong></p></td>
<td align="left"><p> (IPv6 接收段合并) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

有关使用枚举关键字的详细信息，请参阅 [枚举关键字](enumeration-keywords.md)。

 

 





