---
title: WMI 属性限定符
description: WMI 属性限定符
keywords:
- MOF 属性限定符 WDK WMI
- 属性限定符 WDK WMI
- 限定符 WDK WMI
- 标准 MOF 限定符 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b4fee1e63adbf5eba3c1a0b5a020ec139e0ab6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782655"
---
# <a name="wmi-property-qualifiers"></a>WMI 属性限定符





下表列出了可用于在 WMI 数据或事件块中定义项目的必需和可选 MOF 属性限定符。

下面是标准 MOF 限定符： **key**、 **read**、 **write**、 **ValueMap** 和 **Values**。 有关这些和其他标准 MOF 限定符的详细信息，请参阅 [MOF 数据类型](/windows/desktop/WmiSdk/mof-data-types)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>限定符</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>key </p></td>
<td><p>指示数据项是唯一标识类的每个实例的键属性。 只有 InstanceName 属性才能声明为密钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>读取</strong></p></td>
<td><p>指示 WMI 客户端可以读取数据项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>写入</strong></p></td>
<td><p>指示 WMI 客户端可以设置数据项。</p></td>
</tr>
<tr class="even">
<td><p><strong>图</strong></p></td>
<td><p>指定在 <strong>BitValues</strong>中指定的相应字符串值的位位置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BitValues</strong></p></td>
<td><p>指定 (标志名称的字符串值的列表，) 表示数据项中设置的位。 标志的位位置由 <strong>BitMap</strong>中指定的相应位置定义。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefineValues</strong></p></td>
<td><p>指定 WMI 工具套件编译为相应的 #define 语句列表的枚举列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisplayInHex</strong></p></td>
<td><p>指定显示属性值的任何 WMI 客户端都应以十六进制形式执行此操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisplayName ( "</strong><em>string</em><strong>" ) </strong></p></td>
<td><p>指定 WMI 客户端可以用来显示为属性名称的标题。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxLen (</strong> <em>uint</em> <strong>) </strong></p></td>
<td><p>对于字符串属性， <strong>MaxLen</strong> 指定字符串的最大长度（字符）。 <em>Uint</em>值可以是任意32位无符号整数。 如果省略 MaxLen，或者 <em>uint</em> 为零，则字符串的长度不受限制。</p></td>
</tr>
<tr class="even">
<td><p><strong>值</strong></p></td>
<td><p>为此数据项指定可能值的列表。 如果数据项是枚举，则 <strong>ValueMap</strong> 包含与 " <strong>值</strong>" 中指定的枚举值相对应的索引值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ValueMap</strong></p></td>
<td><p>指定 <strong>值</strong>中相应字符串值的整数值。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiDataId (</strong>数据项<em>ID</em> <strong>) </strong></p></td>
<td><p> (必需) 标识数据块中的数据项。 必须将数据项 Id 分配给块中的所有项，所需的项目为 <strong>InstanceName</strong> 和 <strong>Active</strong>。 必须从1开始，在一个连续系列中分配数据项 Id。 项的数据 ID 决定项在数据块的实例中的显示顺序;MOF 类定义中的项的顺序是不相关的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiMethodId (</strong><strong>) </strong> <em>的方法</em></p></td>
<td><p>标识数据块中的方法。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiSizeIs ( "</strong><em>数据项-name</em><strong>" ) </strong></p></td>
<td><p>指定此块中其他数据项的名称，该数据项指示此数据项处可变长度数组中的元素数。 <strong>WmiSizeIs</strong> 仅对定义数组的数据项有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiScale (</strong><em>缩放</em><strong>) </strong></p></td>
<td><p>指定在返回此数据项的值时，驱动程序所使用的缩放系数，以10为幂。 例如，如果 <em>缩放因子</em> 为5，则驱动程序返回的值乘以10⁵。 如果省略 <strong>WmiScale</strong> ，则可将 <em>缩放因子</em> 视为0。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiTimeStamp</strong></p></td>
<td><p>指定64位数据项是自1/1/1601 以来100纳秒的时间戳。 <strong>WmiTimeStamp</strong> 仅对64位数据项有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiComplexity (</strong><em>级别</em><strong>) </strong></p></td>
<td><p>指定一个整数值，该值表示数据项的用户复杂性级别。 WMI 客户端可以使用该值来区分应该提供给初级用户的数据项和应限制为更高级用户的数据项。 0表示最小值，较高的值表示用户的复杂性更高。 如果未指定，则<strong>WmiComplexity</strong>默认为零。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiVolatility (</strong><em>间隔</em><strong>) </strong></p></td>
<td><p>指定此数据项的更新之间的间隔（以毫秒为单位）。 例如，如果每秒更新一次数据项，则 <em>interval</em> 将为1000。 WMI 客户端可能会检查 <strong>WmiVolatility</strong> ，以确定查询可能新值的频率。 如果省略 <strong>WmiVolatility</strong> ，则 <em>interval</em> 为 undefined。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiEventTrigger (</strong> <strong>"</strong> <em>数据项-name</em><strong>" ) </strong></p></td>
<td><p>指定事件块中的数据项的名称，WMI 客户端可以设置该名称来定义事件的触发器值。 例如，如果事件 TooHot 是使用 <strong>WmiEventTrigger</strong> ( "TooHotTemperature" ) 限定的，则 WMI 客户端可以将 TooHotTemperature 设置为指示驱动程序在设备到达 TooHot 的用户指定值时发送 TooHotTemperature 事件。 通常，驱动程序会定义触发器值。 通过公开 <strong>WmiEventTrigger</strong> 数据项，驱动程序允许客户端控制何时触发特定事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiEventRate ( "</strong><em>数据项-name</em><strong>" ) </strong></p></td>
<td><p>指定事件块中数据项的名称，WMI 客户端可以设置该名称来控制发送此事件的频率。 例如，如果数据项目 TooHot 是使用 <strong>WmiEventRate ( "</strong>SendEventRate<strong>" ) </strong>限定的，则 WMI 客户端用户可以将 SendEventRate 设置为指示驱动程序以用户指定的时间间隔发送 TooHot。</p></td>
</tr>
</tbody>
</table>

 

 

