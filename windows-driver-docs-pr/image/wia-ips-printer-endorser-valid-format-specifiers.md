---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效的 \_ 格式 \_ 说明符
description: WIA \_ ips \_ printer \_ ENDORSER \_ 有效 \_ 格式 \_ 说明符属性列出了可嵌入到 WIA \_ IPS \_ PRINTER \_ ENDORSER \_ string 属性的字符串值中的有效特殊格式字符序列。
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_FORMAT_SPECIFIERS 图像设备
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
ms.openlocfilehash: b6d660124b937d64521ae845a5fec06c6b60f659
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783215"
---
# <a name="wia_ips_printer_endorser_valid_format_specifiers"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效的 \_ 格式 \_ 说明符


**Wia \_ ips \_ printer \_ ENDORSER \_ 有效 \_ 格式 \_ 说明符** 属性列出了可嵌入到 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ string**](wia-ips-printer-endorser-string.md)属性的字符串值中的有效特殊格式字符序列。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了对 **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效 \_ 格式 \_ 说明符** 属性有效的常量。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>格式字符串</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PRINT_DATE</p></td>
<td><p>L "$DATE $"</p></td>
<td><p>计算机区域设置格式的当前日期。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_YEAR</p></td>
<td><p>L "$YEAR $"</p></td>
<td><p>当前年份 (4 位数) 。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_MONTH</p></td>
<td><p>L "$MONTH $"</p></td>
<td><p>当月 (1-12) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_DAY</p></td>
<td><p>L "$DAY $"</p></td>
<td><p>月份的当前日期 (1-31) 。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_WEEK_DAY</p></td>
<td><p>L "$WEEK _DAY $"</p></td>
<td><p>在计算机区域设置语言中 (星期几的名称（例如，"星期三" ) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_TIME_24H</p></td>
<td><p>L "$HOUR _24H $"</p></td>
<td><p>以24小时格式 (0-23) 的当前小时。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_TIME_12H</p></td>
<td><p>L "$ TIME_12H $"</p></td>
<td><p>计算机区域设置格式的当前时间，12小时 (上午/P.M. ) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_HOUR_12H</p></td>
<td><p>L "$HOUR _12H $"</p></td>
<td><p>当前早上/P.M。 )  (0-11。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_AM_PM</p></td>
<td><p>L "$AM _PM $"</p></td>
<td><p>"AM" 或 "PM"。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_MINUTE</p></td>
<td><p>L "$MINUTE $"</p></td>
<td><p>当前分钟 (0-59) 。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_SECOND</p></td>
<td><p>L "$SECOND $"</p></td>
<td><p>当前第二 (0-59) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_PAGE_COUNT</p></td>
<td><p>L "$PAGE _COUNT $"</p></td>
<td><p>每个作业)  (页面计数器的值。</p></td>
</tr>
</tbody>
</table>

 

特殊序列 L $ $ 表示 "$" 字符。

对于 Imprinter/Endorser 数据源项，此属性是可选的。 不支持意味着 printer/endorser 设备不支持任何特殊的格式序列。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





