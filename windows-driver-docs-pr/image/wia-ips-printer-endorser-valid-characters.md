---
title: WIA\_IPS\_打印机\_印记签署器\_有效\_字符
description: WIA\_IPS\_打印机\_印记签署器\_有效\_字符属性列出了适用于 WIA 的字符 （字母、 数字、 标点符号和等等）\_IP\_打印机\_印记签署器\_可以为印刷器/印记签署器配置的字符串值。
ms.assetid: 763355B8-7CA0-4B3F-87B1-BD51F24CF78C
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_CHARACTERS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_VALID_CHARACTERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c65c9ab5bbdf94c3d4d2859910cfa9f003b95c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360037"
---
# <a name="wiaipsprinterendorservalidcharacters"></a>WIA\_IPS\_打印机\_印记签署器\_有效\_字符


**WIA\_IPS\_打印机\_印记签署器\_VALID\_字符**属性列出了有效的字符 （字母、 数字、 标点符号和等等）[ **WIA\_IPS\_打印机\_印记签署器\_字符串**](wia-ips-printer-endorser-string.md)可以为印刷器/印记签署器配置的值。 有效的字符组指定为以 NULL 结尾的字符串。 WIA 微型驱动程序创建并维护此属性。




**请注意**  此属性替换[ **WIA\_DPS\_印记签署器\_字符**](wia-dps-endorser-characters.md)，现已过时。

 

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

印刷器/印记签署器的所有项必须都支持中发生的所有字符[ **WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符**](wia-ips-printer-endorser-valid-format-specifiers.md)值 （如果有），包括 $ 字符。 如果印刷器/印记签署器支持 WiaImgFmt\_CSV 值[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)，则、 （逗号） 字符必须不会列出通过**WIA\_IPS\_打印机\_印记签署器\_有效\_字符**。

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


[**WIA\_DPS\_印记签署器\_字符**](wia-dps-endorser-characters.md)

[**WIA\_IPS\_打印机\_印记签署器\_有效\_格式\_说明符**](wia-ips-printer-endorser-valid-format-specifiers.md)

 

 






