---
title: 数据包合并的标准化 INF 关键字
description: 数据包合并的标准化 INF 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1aa7616c3021fe185094320a12e4fb150caaac7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840265"
---
# <a name="standardized-inf-keywords-for-packet-coalescing"></a>数据包合并的标准化 INF 关键字


定义了标准化的 INF 关键字，以启用或禁用微型端口驱动程序上的数据包合并支持。

支持数据包合并的适配器的微型端口驱动程序的 INF 文件必须指定 **\* PACKETCOALESCING** 标准化 INF 关键字。 安装驱动程序后，管理员可以在适配器的 "**高级**" 属性页中更新 **\* PacketCoalescing** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

**\* PacketCoalescing** INF 关键字是一个枚举关键字。 下表描述了 **\* PacketCoalescing** inf 关键字的可能 inf 条目。 此表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的 **NDI \\ params \\** 键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。

 

<a href="" id="value"></a>“值”  
与列表中的每个 SubkeyName 相关联的枚举整数值。

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

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
<td align="left"><p><strong>*PacketCoalescing</strong></p></td>
<td align="left"><p>数据包合并</p></td>
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

 

微型端口驱动程序必须检查注册表中的 **\* PacketCoalescing** 关键字值，然后才会公布其对数据包合并的支持。 如果 **\* PacketCoalescing** 关键字的值为零，则该小型端口不得为任何数据包合并功能公布支持。 有关详细信息，请参阅 [报告数据包合并功能](reporting-packet-coalescing-capabilities.md)。

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





