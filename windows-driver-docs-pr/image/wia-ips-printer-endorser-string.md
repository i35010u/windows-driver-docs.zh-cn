---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 字符串
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ STRING 属性用于配置要打印/认可的文本。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_STRING 图像设备
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
ms.openlocfilehash: 48767fb5e7b79e376f594a752c7c8b3612b98737
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815099"
---
# <a name="wia_ips_printer_endorser_string"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 字符串


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ STRING** 属性用于配置要打印/认可的文本。 WIA 微型驱动程序创建并维护此属性。




**注意**  此属性替换现在已过时的 [**WIA \_ DPS \_ ENDORSER \_ 字符串**](wia-dps-endorser-string.md)。

 

属性类型： VT \_ BSTR

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

要打印/认可的文本可以用一个或多个字符串表示。 每个字符串可以包含一个或多个由 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效 \_ 格式 \_ 说明符**](wia-ips-printer-endorser-valid-format-specifiers.md) 属性描述的特殊字符格式设置序列。 字符串只能包含 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效 \_ 字符**](wia-ips-printer-endorser-valid-characters.md) 指定的字符，并且必须以 NULL 结尾。 当配置多个字符串时，WIA 微型驱动程序必须在新页面上打印/认可每个字符串 (在) 的字符串列表中循环。

对于所有 Imprinter/Endorser 数据源项，此属性是可选的。

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


[**WIA \_ DPS \_ ENDORSER \_ 字符串**](wia-dps-endorser-string.md)

 

 






