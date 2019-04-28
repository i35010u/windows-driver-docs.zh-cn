---
title: WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符
description: WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符属性列表的有效特殊格式设置字符序列可以嵌入在字符字符串值为 WIA\_IPS\_打印机\_印记签署器\_字符串属性。
ms.assetid: D7D6BA47-623A-4F8F-9E29-2C9043AD4C2F
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_FORMAT_SPECIFIERS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_VALID_FORMAT_SPECIFIERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ef6b7f9e5404fe827c2b8a893b1ca40223fac8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351099"
---
# <a name="wiaipsprinterendorservalidformatspecifiers"></a>WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符


**WIA\_IPS\_打印机\_印记签署器\_VALID\_格式\_说明符**属性列出了有效的特殊格式设置字符序列要嵌入的字符串值[ **WIA\_IPS\_打印机\_印记签署器\_字符串**](wia-ips-printer-endorser-string.md)属性。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了对有效的常量**WIA\_IPS\_打印机\_印记签署器\_VALID\_格式\_说明符**属性。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>格式字符串</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PRINT_DATE</p></td>
<td><p>L"$DATE$"</p></td>
<td><p>区域设置格式的计算机中的当前日期。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_YEAR</p></td>
<td><p>L"$YEAR$"</p></td>
<td><p>当前年份 （4 位数字）。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_MONTH</p></td>
<td><p>L"$MONTH$"</p></td>
<td><p>当前月份 (1-12)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_DAY</p></td>
<td><p>L"$DAY$"</p></td>
<td><p>当前日期的月份 (1-31)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_WEEK_DAY</p></td>
<td><p>L"$WEEK_DAY$"</p></td>
<td><p>当前日期 （例如，"Wednesday"） 计算机区域设置语言中星期几的名称。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_TIME_24H</p></td>
<td><p>L"$HOUR_24H$"</p></td>
<td><p>当前小时采用 24 小时格式 (0-23)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_TIME_12H</p></td>
<td><p>L"$ TIME_12H$"</p></td>
<td><p>计算机区域设置的当前时间设置的格式，12 小时 （12 小时制）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_HOUR_12H</p></td>
<td><p>L"$HOUR_12H$"</p></td>
<td><p>当前的 a.m./p.m.。 小时 (0-11)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_AM_PM</p></td>
<td><p>L"$AM_PM$"</p></td>
<td><p>"AM"或者"PM"。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_MINUTE</p></td>
<td><p>L"$MINUTE$"</p></td>
<td><p>当前分钟 (0-59)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_SECOND</p></td>
<td><p>L"第二个 $$"</p></td>
<td><p>当前秒 (0-59)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_PAGE_COUNT</p></td>
<td><p>L"$PAGE_COUNT$"</p></td>
<td><p>（每个作业） 的页计数器的值。</p></td>
</tr>
</tbody>
</table>

 

特殊顺序 L"$$"表示 $ 字符。

此属性是可选的印刷器/印记签署器数据源项。 打印机/印记签署器设备不支持任何特殊的格式不受支持的方法序列。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





