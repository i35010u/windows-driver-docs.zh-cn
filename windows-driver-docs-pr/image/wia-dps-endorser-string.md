---
title: WIA \_ DPS \_ ENDORSER \_ 字符串
description: WIA \_ DPS \_ ENDORSER \_ string 属性包含一个字符串，该字符串将被认可 (也就是说，在微型驱动程序扫描的每一页上打印) 。
keywords:
- WIA_DPS_ENDORSER_STRING 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_ENDORSER_STRING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58180e07f1d4a379b6a2d30c1c1f3e06e52cc159
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836989"
---
# <a name="wia_dps_endorser_string"></a>WIA \_ DPS \_ ENDORSER \_ 字符串


WIA \_ DPS \_ ENDORSER \_ string 属性包含一个字符串，该字符串将被认可 (也就是说，在微型驱动程序扫描的每一页上打印) 。

## <span id="ddk_wia_dps_endorser_string_si"></span><span id="DDK_WIA_DPS_ENDORSER_STRING_SI"></span>


**注意**  此属性现已过时。 请改用 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ STRING**](wia-ips-printer-endorser-string.md) 。

 

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序 \_ \_ \_ 通过使用在 " [**wia \_ dps \_ ENDORSER \_ 字符**](wia-dps-endorser-characters.md) " 属性中报告的有效字符集来设置 wia dps ENDORSER 字符串属性。 如果在 WIA \_ DPS ENDORSER 字符串中设置了字符串，WIA 微型驱动程序应仅对文档进行签署 \_ \_ 。 空字符串表示禁用了 endorser 功能。

由于驱动程序必须解释 endorser 字符串，因此，驱动程序可以在 WIA \_ DPS endorser 字符串中使用特殊字符 \_ \_ 。 但是，只有您的应用程序才能理解这些字符。

支持 WIA \_ DPS \_ ENDORSER 字符串属性的驱动程序 \_ 必须支持以下标记列表：

<span id="_DATE__"></span><span id="_date__"></span>$DATE $   
日期格式为 YYYY/MM/DD。

<span id="_DAY__"></span><span id="_day__"></span>$DAY $   
日，格式为 DD。

<span id="_MONTH__"></span><span id="_month__"></span>$MONTH $   
一年中的月份，格式为 MM。

<span id="_PAGE_COUNT__"></span><span id="_page_count__"></span>$PAGE \_ 计数 $   
传输的页数。

<span id="_TIME__"></span><span id="_time__"></span>$TIME $   
当天的时间，格式为 HH： MM： SS。

<span id="_YEAR__"></span><span id="_year__"></span>$YEAR $   
年份，格式为 YYYY。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ ENDORSER \_ 字符**](wia-dps-endorser-characters.md)

[**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 字符串**](wia-ips-printer-endorser-string.md)

 

 






