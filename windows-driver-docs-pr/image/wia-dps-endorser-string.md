---
title: WIA\_DPS\_印记签署器\_字符串
description: WIA\_DPS\_印记签署器\_字符串属性中包含的字符串进行认可 （打印） 的微型驱动程序会扫描每个页上。
ms.assetid: c51a2941-9101-4749-8fa7-b9f3bbcb0803
keywords:
- WIA_DPS_ENDORSER_STRING 成像设备
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
ms.openlocfilehash: c0df4751804fe5054ccff7c6707ed3fdda124480
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369577"
---
# <a name="wiadpsendorserstring"></a>WIA\_DPS\_印记签署器\_字符串


WIA\_DPS\_印记签署器\_字符串属性中包含的字符串进行认可 （打印） 的微型驱动程序会扫描每个页上。

## <span id="ddk_wia_dps_endorser_string_si"></span><span id="DDK_WIA_DPS_ENDORSER_STRING_SI"></span>


**请注意**  此属性现已过时。 使用[ **WIA\_IPS\_打印机\_印记签署器\_字符串**](wia-ips-printer-endorser-string.md)相反。

 

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_DPS\_印记签署器\_使用，它是设置的有效字符的字符串属性中报告[ **WIA\_DPS\_印记签署器\_字符**](wia-dps-endorser-characters.md)属性。 WIA 微型驱动程序应认可文档中 WIA 设置一个字符串，才\_DPS\_印记签署器\_字符串。 空字符串表示的印记签署器功能处于禁用状态。

由于驱动程序必须解释印记签署器字符串，您的驱动程序可以在 WIA 中使用特殊字符\_DPS\_印记签署器\_字符串。 但是，只有你的应用程序将了解这些字符。

驱动程序支持 WIA\_DPS\_印记签署器\_字符串属性必须支持以下令牌列表：

<span id="_DATE__"></span><span id="_date__"></span>$DATE $   
在窗体 YYYY/MM/dd。 日期

<span id="_DAY__"></span><span id="_day__"></span>$DAY $   
一天，在窗体 dd。

<span id="_MONTH__"></span><span id="_month__"></span>$MONTH $   
MM 窗体中每年的月份。

<span id="_PAGE_COUNT__"></span><span id="_page_count__"></span>$PAGE\_计数 $   
已传输的页数。

<span id="_TIME__"></span><span id="_time__"></span>$TIME $   
一天，hh: mm： 在窗体中的时间。

<span id="_YEAR__"></span><span id="_year__"></span>$YEAR $   
YYYY 窗体中的年份。

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

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_印记签署器\_字符**](wia-dps-endorser-characters.md)

[**WIA\_IPS\_PRINTER\_ENDORSER\_STRING**](wia-ips-printer-endorser-string.md)

 

 






