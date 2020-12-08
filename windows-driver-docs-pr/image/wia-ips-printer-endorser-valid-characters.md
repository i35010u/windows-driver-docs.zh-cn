---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 有效 \_ 字符
description: WIA \_ ips \_ printer \_ ENDORSER \_ 有效 \_ 字符属性列出了字符 (字母、数字、标点符号等) ，这些字符对于可为 \_ \_ \_ Imprinter/ENDORSER 配置的 WIA IPS 打印机 ENDORSER \_ 字符串值有效。
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_CHARACTERS 图像设备
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
ms.openlocfilehash: e9858a9b78a0ade844a92569bfdccad75cc8b708
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795511"
---
# <a name="wia_ips_printer_endorser_valid_characters"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 有效 \_ 字符


**Wia \_ ips \_ printer \_ ENDORSER \_ 有效 \_ 字符** 属性列出了字符 (字母、数字、标点符号等) ，这些字符对于可为 Imprinter/ENDORSER 配置的 [**WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 字符串**](wia-ips-printer-endorser-string.md)值有效。 有效字符集指定为以 NULL 结尾的字符串。 WIA 微型驱动程序创建并维护此属性。




**注意**  此属性替换当前已过时的 [**WIA \_ DPS \_ ENDORSER \_ 字符**](wia-dps-endorser-characters.md)。

 

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

所有 Imprinter/Endorser 项都必须支持 [**WIA \_ IPS \_ 打印机 \_ Endorser \_ 有效 \_ 格式 \_ 说明符**](wia-ips-printer-endorser-valid-format-specifiers.md) 值中出现的所有字符（包括 "$" 字符）)  (。 如果 Imprinter/Endorser 支持 \_ [**wia \_ IPA \_ TYMED**](wia-ipa-tymed.md)的 WiaImgFmt CSV 值， **wia IPS PRINTER Endorser 的 "，" (逗号) 字符不得由 \_ \_ \_ \_ 无效 \_ 字符** 列出。

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


[**WIA \_ DPS \_ ENDORSER \_ 字符**](wia-dps-endorser-characters.md)

[**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 有效的 \_ 格式 \_ 说明符**](wia-ips-printer-endorser-valid-format-specifiers.md)

 

 






