---
title: RSC 的标准化 INF 关键字
description: RSC 的标准化 INF 关键字
ms.assetid: 7418E02F-FD5A-4E58-AAA5-3055B98ED264
keywords:
- 接收方合并 WDK 网络标准化 INF 关键字
- RSC WDK 网络、 标准化 INF 关键字
- WDK RSC 的标准化的 INF 关键字
- INF 条目 WDK RSC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79485aa6f41f1160026353f2b399ad134e8bedfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390657"
---
# <a name="standardized-inf-keywords-for-rsc"></a>RSC 的标准化 INF 关键字





在 Windows 8 中，Windows Server 2012，及更高版本，接收段合并 (RSC) 接口支持[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)，出现在注册表和 INF 文件中指定。

以下列表显示了枚举[标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)适用于 RSC:

<a href="" id="-rscipv4"></a>**\*RscIPv4**  
启用或禁用对 IPv4 数据报版本的 RSC 的支持。

<a href="" id="---------rscipv6"></a> **\*RscIPv6**  
启用或禁用对 IPv6 数据报版本的 RSC 的支持。

枚举标准化 INF 关键字具有以下属性：

<a href="" id="subkeyname"></a>**SubkeyName**  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>**ParamDesc**  
与之关联的显示文本**SubkeyName**。

<a href="" id="value"></a>**值**  
在列表中每个选项与关联枚举的整数值。 此值存储在 NDI\\params\\ *SubkeyName*\\*值*。

<a href="" id="enumdesc"></a>**EnumDesc**  
与每个菜单中显示的值相关联的显示文本。

<a href="" id="default"></a>**默认值**  
菜单默认值。

下表描述了可能的 INF 项 RSC 枚举关键字。

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
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>RscIPv4</strong></p></td>
<td align="left"><p>接收段合并 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>RscIPv6</strong></p></td>
<td align="left"><p>接收段合并 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

有关使用枚举关键字的详细信息，请参阅[枚举关键字](enumeration-keywords.md)。

 

 





