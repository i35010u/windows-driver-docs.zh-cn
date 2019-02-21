---
title: 驱动程序定义的 WMI 数据项目
description: 驱动程序定义的 WMI 数据项目
ms.assetid: 97b64571-95ff-4d61-9fa0-5690e9f29345
keywords:
- 数据类型 WDK WMI
- 嵌入的 WDK WMI 类
- 数据项 WDK WMI
- WMI WDK 内核，驱动程序定义的数据的项
- 驱动程序定义的数据的项 WDK WMI
- WDK WMI 类
- WMI WDK 内核类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f60b9b54329682edccfbc81fea01b995d3fa48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533255"
---
# <a name="driver-defined-wmi-data-items"></a>驱动程序定义的 WMI 数据项目





WMI 数据或事件块的类定义中的数据项可以是以下值之一：

-   基本数据类型，如字符串或无符号的整数。

-   嵌入的类。 嵌入的类仅用作另一个类定义中的数据项并不公开为数据块或事件块。

-   基本数据类型或嵌入的类的一个固定长度或可变长度数组。

将数据块发送给 WMI，驱动程序必须对齐 8 字节边界上的块的开头。 块中的所有后续数据项必须对齐上的数据类型的相应对齐方式。 一个**布尔**或**uint8**的 1 字节边界上对齐。 一个**sint16**， **uint16**，或**字符串**项应对齐 2 字节边界，依次类推。 数组应对齐基于数组的基类型。 应在字节边界上对齐的字节数组，数组 uint64 应对齐 8 字节边界，依次类推。 嵌入的类应对齐在被定义为嵌入类中的最大元素的嵌入类的自然对齐方式的基础。 例如，如果嵌入的类具有**uint64**，类的 8 字节边界上对齐。 WMI 数据项对齐遵循相同的约定 **/zp8** Microsoft C 编译器开关。

驱动程序编写器不一定需要定义所需的项以外的块中的数据项**InstanceName**并**Active**。 例如，一个空事件块可用作通知发生了一个事件，而无需额外的数据。 或数据块可能只需枚举响应中的实例名称[ **IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)请求。

下表列出了可用于定义在 WMI 数据或事件块中的项的 MOF 数据类型。 有关 MOF 的数据类型的详细信息，请参阅 Microsoft Windows SDK。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>数据类型</th>
<th>数据格式</th>
<th>对齐方式 （以字节为单位）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>string</strong></p></td>
<td><p>指定的字符串长度以字节为单位，Unicode 字符串数据后跟 USHORT。 字符串数据可以根据需要包含后跟填充终止 0。 如果是这样，字符串长度必须包括终止 0 和填充。 驱动程序可以使用<strong>MaxLen</strong>限定符以字符串的字符为单位指定的最大长度。 指定最大字符串长度的驱动程序可以使用固定的大小缓冲区来存放字符串。 如果字符串为严格小于缓冲区的大小，该驱动程序可以填充了零的字符串的其余部分。</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>boolean</strong></p></td>
<td><p>一个字节值 0 为 FALSE 的位置和任何非零值为 TRUE</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint8</strong></p></td>
<td><p>8 位有符号整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>uint8</strong></p></td>
<td><p>8 位无符号的整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint16</strong></p></td>
<td><p>16 位有符号整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>uint16</strong></p></td>
<td><p>16 位无符号的整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint32</strong></p></td>
<td><p>32 位有符号整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p><strong>uint32</strong></p></td>
<td><p>32 位无符号的整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint64</strong></p></td>
<td><p>64 位有符号整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p><strong>uint64</strong></p></td>
<td><p>64 位无符号的整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>datetime</strong></p></td>
<td><p>一个指定的绝对日期或时间间隔的定长 25 个字符 Unicode 字符串。 一个<strong>datetime</strong>值具有以下格式：</p>
<p><em>yyyymmddhhmmss.mmmmmmsutc</em></p>
<p>其中：</p>
<p><em>yyyy</em>是 4 位数的年份</p>
<p><em>mm</em>是 2 位数的月份</p>
<p><em>dd</em>是月份中的 2 位数的日期</p>
<p><em>hh</em>是根据 24 小时制的小时</p>
<p><em>mm</em>分钟</p>
<p><em>ss</em>秒数</p>
<p><em>表示</em>是微秒数</p>
<p><em>s</em>加号 （+） 或减号 （-），该值指示是否<em>utc</em>是正或负偏移量从协调世界时; 或一个冒号 （:），该值指示<strong>datetime</strong>值是时间间隔。</p>
<p><em>utc</em>是以分钟为单位从通用时间坐标的偏移量。 如果<em>utc</em>为零 (000) <strong>datetime</strong>值是一个时间间隔。</p>
<p>值必须是零填充。 意义不大的字段可以填充带星号 （*）。</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

 

 

 




