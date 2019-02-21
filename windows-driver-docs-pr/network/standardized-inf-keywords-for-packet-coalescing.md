---
title: 数据包合并的标准化的 INF 关键字
description: 数据包合并的标准化的 INF 关键字
ms.assetid: 423E9B50-6474-454A-97BB-91404DF9F729
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76402d713dcde5ea18730920425a1e5b45574c70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521464"
---
# <a name="standardized-inf-keywords-for-packet-coalescing"></a>数据包合并的标准化的 INF 关键字


标准化的 INF 关键字定义来启用或禁用对数据包合并微型端口驱动程序的支持。

支持数据包合并的适配器的微型端口驱动程序的 INF 文件必须指定 **\*PacketCoalescing**标准化 INF 关键字。 安装该驱动程序后，管理员可以更新 **\*PacketCoalescing**中的关键字值**高级**适配器属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**  中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

 **\*PacketCoalescing** INF 关键字是一个枚举的关键字。 下表描述了可能 INF 条目 **\*PacketCoalescing** INF 关键字。 此表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表**NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

**请注意**  独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="value"></a>值  
枚举的整数值与列表中每个 SubkeyName 相关联。

<a href="" id="enumdesc"></a>EnumDesc  
与每个菜单中显示的值相关联的显示文本。

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
<td align="left"><p><strong>*PacketCoalescing</strong></p></td>
<td align="left"><p>数据包合并</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序必须检查 **\*PacketCoalescing**之前也会公布它对数据包合并的支持在注册表中的关键字值。 如果 **\*PacketCoalescing**关键字的值为零、 微型端口必须不播发任何数据包合并功能的支持。 有关详细信息，请参阅[报告数据包合并功能](reporting-packet-coalescing-capabilities.md)。

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





