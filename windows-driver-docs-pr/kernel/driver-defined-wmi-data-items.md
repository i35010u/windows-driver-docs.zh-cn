---
title: 驱动程序定义的 WMI 数据项
description: 驱动程序定义的 WMI 数据项
ms.assetid: 97b64571-95ff-4d61-9fa0-5690e9f29345
keywords:
- 数据类型 WDK WMI
- embedded 类 WDK WMI
- 数据项 WDK WMI
- WMI WDK 内核，驱动程序定义的数据项
- 驱动程序定义的数据项 WDK WMI
- 类 WDK WMI
- WMI WDK 内核，类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5ca4b872661af512d1727bf11fbb8cd2fe3306
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192705"
---
# <a name="driver-defined-wmi-data-items"></a>驱动程序定义的 WMI 数据项





WMI 数据或事件块的类定义中的数据项可以是以下项之一：

-   基本数据类型，如字符串或无符号整数。

-   嵌入的类。 嵌入类仅用作另一类定义中的数据项，不作为数据块或事件块公开。

-   基本数据类型或嵌入类的固定长度或可变长度数组。

将数据块发送到 WMI 时，驱动程序必须将块的开头与8字节边界对齐。 块中的所有后续数据项必须与数据类型的相应对齐方式对齐。 **布尔值**或**uint8**应在1字节边界上对齐。 **Sint16**、 **uint16**或**string**项应在2字节边界上对齐，依此类推。 数组应基于数组的基类型对齐。 字节数组应在字节边界上对齐，uint64 数组应在8字节边界上对齐，依此类推。 嵌入类应根据嵌入类的自然对齐方式对齐，该嵌入类定义为嵌入类中的最大元素。 例如，如果嵌入类具有 **uint64**，则类应在8字节边界上对齐。 WMI 数据项对齐遵循与 Microsoft C 编译器上的 **了/zp8** 开关相同的约定。

驱动程序编写器不一定必须在所需的项 **InstanceName** 和 **Active**块中定义数据项。 例如，空事件块可以用作事件发生的通知，而无需额外的数据。 或者，数据块可能只是枚举实例名称以响应 [**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**](./irp-mn-query-all-data.md) 请求。

下表列出了可用于在 WMI 数据或事件块中定义项的 MOF 数据类型。 有关 MOF 数据类型的详细信息，请参阅 Microsoft Windows SDK。

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
<th>对齐 (字节) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>string</strong></p></td>
<td><p>一个 USHORT，它指定字符串的长度（以字节为单位），后跟 Unicode 字符串数据。 字符串数据可以有选择性地包括终止0后跟填充。 如果是这样，则字符串长度必须包含终止0和填充。 驱动程序可以使用 <strong>MaxLen</strong> 限定符来指定字符串的最大长度（字符）。 指定最大字符串长度的驱动程序可以使用固定大小的缓冲区来保存字符串。 如果字符串严格小于缓冲区的大小，则驱动程序可以用零填充字符串的其余部分。</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>boolean</strong></p></td>
<td><p>单字节值，其中0为 FALSE，任何非零值为 TRUE</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint8</strong></p></td>
<td><p>8 位带符号整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>uint8</strong></p></td>
<td><p>无符号的 8 位整数</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint16</strong></p></td>
<td><p>有符号 16 位整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p><strong>uint16</strong></p></td>
<td><p>无符号 16 位整数</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint32</strong></p></td>
<td><p>带符号的 32 位整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p>uint32</p></td>
<td><p>无符号的 32 位整数</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>sint64</strong></p></td>
<td><p>64 位带符号整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>uint64</p></td>
<td><p>无符号 64 位整数</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>datetime</strong></p></td>
<td><p>固定长度25个字符的 Unicode 字符串，用于指定绝对日期或时间间隔。 <strong>Datetime</strong>值采用以下格式：</p>
<p><em>yyyymmddhhmmss. mmmmmmsutc</em></p>
<p>其中：</p>
<p><em>yyyy</em> 为四位数年份</p>
<p><em>mm</em> 是两位数月份</p>
<p><em>dd</em> 是月中的两位数日期</p>
<p><em>hh</em> 是根据24小时制的小时</p>
<p><em>mm</em> 为分钟</p>
<p><em>ss</em> 是秒</p>
<p><em>mmmmmm</em> 是微秒数</p>
<p><em>s</em> 是加号 (+) 或减号 (-) ，指示 <em>utc</em> 是相对于通用时间坐标的正负偏移量;或冒号 (： ) ，它指示 <strong>datetime</strong> 值为时间间隔。</p>
<p><em>utc</em> 是指从通用时间坐标开始的偏移量（分钟）。 如果 <em>utc</em> 为零 (000) ，则 <strong>datetime</strong> 值为 interval。</p>
<p>值必须填充零。 不太重要的字段可以用星号 ( * ) 来填充。</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

 

 

