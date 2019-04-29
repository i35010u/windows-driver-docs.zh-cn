---
title: WMI 属性限定符
description: WMI 属性限定符
ms.assetid: e2d281b3-913c-43ad-921c-80dc8be09aa0
keywords:
- MOF 属性限定符 WDK WMI
- 属性限定符 WDK WMI
- WDK WMI 限定符
- 标准 MOF 限定符 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86dd32e25cfe4a16e8a0c379abed235015420850
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327227"
---
# <a name="wmi-property-qualifiers"></a>WMI 属性限定符





下表列出了必需和可选 MOF 属性限定符可用于定义在 WMI 数据或事件块中的项。

以下是标准 MOF 限定符：**键**，**读取**，**编写**， **ValueMap**，并**值**. 有关这些和其他标准 MOF 限定符的详细信息，请参阅[MOF 数据类型](https://msdn.microsoft.com/library/aa392392)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>限定符</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>key</strong></p></td>
<td><p>指示数据项是唯一标识类的每个实例的键属性。 InstanceName 属性可以声明一个键。</p></td>
</tr>
<tr class="even">
<td><p><strong>read</strong></p></td>
<td><p>表示 WMI 客户端可以读取的数据项目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>write</strong></p></td>
<td><p>表示 WMI 客户端可以设置数据项。</p></td>
</tr>
<tr class="even">
<td><p><strong>BitMap</strong></p></td>
<td><p>指定相应的字符串值中指定的位位置<strong>BitValues</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>BitValues</strong></p></td>
<td><p>指定字符串表示位数据项中设置的值 （标记名称） 的列表。 一个标志的位位置定义的相应位置中指定<strong>位图</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefineValues</strong></p></td>
<td><p>指定的 WMI 工具套件将编译为相应的列表的枚举的列表 #define 语句。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisplayInHex</strong></p></td>
<td><p>指定显示的属性值的任何 WMI 客户端应该操作以十六进制格式。</p></td>
</tr>
<tr class="even">
<td><p><strong>DisplayName("</strong><em>string</em><strong>")</strong></p></td>
<td><p>指定 WMI 客户端可用来显示为属性名称的标题。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxLen(</strong><em>uint</em><strong>)</strong></p></td>
<td><p>对于字符串属性， <strong>MaxLen</strong>以字符为单位指定字符串的最大长度。 <em>Uint</em>值可以是任何 32 位无符号的整数。 如果省略 MaxLen，或<em>uint</em>为零，则该字符串的长度不受限制。</p></td>
</tr>
<tr class="even">
<td><p><strong>值</strong></p></td>
<td><p>指定此数据项的可能值的列表。 如果数据项是一个枚举， <strong>ValueMap</strong>包含对应于枚举值中指定的索引值<strong>值</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ValueMap</strong></p></td>
<td><p>指定在相应的字符串值的整数值<strong>值</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiDataId(</strong><em>data-item-ID</em><strong>)</strong></p></td>
<td><p>（必需）标识数据块中的数据项。 数据项 Id 必须分配到所需的项除外的块中的所有项<strong>InstanceName</strong>并<strong>Active</strong>。 数据项 Id 必须分配在连续系列中，从 1 开始。 项的数据 ID 确定项的数据块，实例中的显示的顺序MOF 类定义中的项的顺序是不相关。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiMethodId(</strong><em>method-item-ID</em><strong>)</strong></p></td>
<td><p>标识数据块中的方法。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiSizeIs("</strong><em>data-item-name</em><strong>")</strong></p></td>
<td><p>在此块中，该值指示在此数据项的可变长度数组中的元素数指定另一个数据项的名称。 <strong>WmiSizeIs</strong>仅对定义数组的数据项有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiScale(</strong><em>scale-factor</em><strong>)</strong></p></td>
<td><p>指定为 10，驱动程序使用时返回此数据项的值的幂缩放比例因子。 例如，如果<em>比例系数</em>为 5，该驱动程序返回的值乘以 10⁵。 如果<strong>WmiScale</strong>省略，则<em>缩放比例</em>可以假定为 0。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiTimeStamp</strong></p></td>
<td><p>指定 64 位的数据项，是自 1601 年 1/1/100 纳秒为单位的时间戳。 <strong>WmiTimeStamp</strong>仅对 64 位的数据项有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiComplexity(</strong><em>level</em><strong>)</strong></p></td>
<td><p>指定一个整数值，表示用户复杂性级别的数据项。 WMI 客户端可以使用该值来区分数据项应可供初学者和应限制为更高级的用户的数据项。 零表示的最小值和较高的值指示更高版本用户的复杂程度。 <strong>WmiComplexity</strong>默认为零，如果未指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiVolatility(</strong><em>interval</em><strong>)</strong></p></td>
<td><p>指定时间间隔，以毫秒为单位，此数据项目的更新间隔。 例如，如果数据项更新一次每个第二个，<em>间隔</em>是 1000年。 WMI 客户端可能会检查<strong>WmiVolatility</strong>来确定经常查询的可能的新值的方式。 如果<strong>WmiVolatility</strong>省略，则<em>间隔</em>是不确定的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WmiEventTrigger(</strong> <strong>"</strong> <em>data-item-name</em><strong>")</strong></p></td>
<td><p>在 WMI 客户端可以设置定义该事件的触发器值的事件块中指定数据项的名称。 例如，如果使用限定事件 TooHot <strong>WmiEventTrigger</strong>("TooHotTemperature")，WMI 客户端可以设置 TooHotTemperature 以指示驱动程序发送 TooHot 事件时设备达到用户指定的值有关 TooHotTemperature。 通常一个驱动程序定义的触发器值。 通过公开<strong>WmiEventTrigger</strong>数据项，驱动程序允许客户端控制何时触发特定事件。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiEventRate("</strong><em>data-item-name</em><strong>")</strong></p></td>
<td><p>WMI 客户端可以用来控制发送此事件的频率事件块中指定数据项的名称。 例如，如果数据项 TooHot 是用限定<strong>WmiEventRate ("</strong>SendEventRate<strong>")</strong>，WMI 客户端用户可以设置 SendEventRate 以指示要在用户指定的时间间隔发送 TooHot 的驱动程序。</p></td>
</tr>
</tbody>
</table>

 

 

 




