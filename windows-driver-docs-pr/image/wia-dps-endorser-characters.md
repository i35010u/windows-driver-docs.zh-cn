---
title: WIA \_ DPS \_ ENDORSER \_ 字符
description: WIA \_ DPS \_ ENDORSER \_ 字符属性包含应用程序可用于创建有效 ENDORSER 字符串的所有有效字符。
keywords:
- WIA_DPS_ENDORSER_CHARACTERS 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_ENDORSER_CHARACTERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e996d9babc419f794bf57cdee8144f2e1b3d9d70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836991"
---
# <a name="wia_dps_endorser_characters"></a>WIA \_ DPS \_ ENDORSER \_ 字符


WIA \_ DPS \_ ENDORSER \_ 字符属性包含应用程序可用于创建有效 ENDORSER 字符串的所有有效字符。

## <span id="ddk_wia_dps_endorser_characters_si"></span><span id="DDK_WIA_DPS_ENDORSER_CHARACTERS_SI"></span>


**注意**  此属性现已过时。 请改用 [**WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 有效 \_ 字符**](wia-ips-printer-endorser-valid-characters.md) 。

 

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

"Endorser" 是安装在扫描仪上的打印机，该扫描程序在扫描的每一页上都有一条短信。 WIA 微型驱动程序应根据 WIA dps ENDORSER 字符属性中的有效字符集验证 [**wia \_ dps \_ ENDORSER \_ STRING**](wia-dps-endorser-string.md) 属性的设置 \_ \_ \_ 。 微型驱动程序创建并维护此属性。

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

[**WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 有效 \_ 字符**](wia-ips-printer-endorser-valid-characters.md)

 

 






