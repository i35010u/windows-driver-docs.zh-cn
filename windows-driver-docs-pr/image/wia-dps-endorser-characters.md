---
title: WIA\_DPS\_印记签署器\_字符
description: WIA\_DPS\_印记签署器\_字符属性包含所有应用程序可以使用创建有效的印记签署器字符串的有效字符。
ms.assetid: 7bf0676b-df85-486b-a448-ab7275ac846d
keywords:
- WIA_DPS_ENDORSER_CHARACTERS 成像设备
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
ms.openlocfilehash: 0dd3008879a607eee4cb494c93b53dd96a74ae06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369573"
---
# <a name="wiadpsendorsercharacters"></a>WIA\_DPS\_印记签署器\_字符


WIA\_DPS\_印记签署器\_字符属性包含所有应用程序可以使用创建有效的印记签署器字符串的有效字符。

## <span id="ddk_wia_dps_endorser_characters_si"></span><span id="DDK_WIA_DPS_ENDORSER_CHARACTERS_SI"></span>


**请注意**  此属性现已过时。 使用[ **WIA\_IPS\_打印机\_印记签署器\_有效\_字符**](wia-ips-printer-endorser-valid-characters.md)相反。

 

属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

"印记签署器"是 imprints 扫描每一页上的短信在扫描程序安装的打印机。 WIA 微型驱动程序应验证的设置[ **WIA\_DPS\_印记签署器\_字符串**](wia-dps-endorser-string.md)在 WIA中设置属性的有效字符与\_DPS\_印记签署器\_字符属性。 微型驱动程序创建并维护此属性。

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

[**WIA\_IPS\_打印机\_印记签署器\_有效\_字符**](wia-ips-printer-endorser-valid-characters.md)

 

 






