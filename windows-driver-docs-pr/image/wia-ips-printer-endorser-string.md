---
title: WIA\_IPS\_打印机\_印记签署器\_字符串
description: WIA\_IPS\_打印机\_印记签署器\_字符串属性用于配置要将打印/认可的文本。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: DF4B1361-EC9C-4BEA-97F5-9179DCB77044
keywords:
- WIA_IPS_PRINTER_ENDORSER_STRING 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_STRING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a30b966b37d4b29fea63899f3f51e9c2f80d625a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351131"
---
# <a name="wiaipsprinterendorserstring"></a>WIA\_IPS\_打印机\_印记签署器\_字符串


**WIA\_IPS\_打印机\_印记签署器\_字符串**属性用于配置要将打印/认可的文本。 WIA 微型驱动程序创建并维护此属性。




**请注意**  此属性替换[ **WIA\_DPS\_印记签署器\_字符串**](wia-dps-endorser-string.md)，现已过时。

 

属性类型：VT\_BSTR

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

可以由一个或多个字符字符串表示要打印/认可的文本。 每个字符的字符串可以包含一个或多个特殊字符格式设置序列所描述[ **WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符**](wia-ips-printer-endorser-valid-format-specifiers.md)属性。 字符串必须包含指定的唯一字符[ **WIA\_IPS\_打印机\_印记签署器\_有效\_字符**](wia-ips-printer-endorser-valid-characters.md)必须终止 NULL。 当配置多个字符字符串时，WIA 微型驱动程序必须打印/赞同将在新页 （循环的字符串列表） 的每个字符串。

此属性是可选的所有印刷器/印记签署器数据源项。

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


[**WIA\_DPS\_印记签署器\_字符串**](wia-dps-endorser-string.md)

 

 






