---
title: WIA\_IPS\_打印机\_印记签署器\_最大\_图形
description: WIA\_IPS\_打印机\_印记签署器\_最大\_图形属性描述每个页面上的最大的印刷器/印记签署器项可以打印或认可的映像数。
ms.assetid: A8FB39D2-659C-45E9-BE5E-627E594B9D3A
keywords:
- WIA_IPS_PRINTER_ENDORSER_MAX_GRAPHICS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_MAX_GRAPHICS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eee3c72973bdbbd14bff590f8ad6199629962238
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520616"
---
# <a name="wiaipsprinterendorsermaxgraphics"></a>WIA\_IPS\_打印机\_印记签署器\_最大\_图形


**WIA\_IPS\_打印机\_印记签署器\_最大\_图形**属性描述图像用于印刷器/印记签署器项可打印的最大数目或认可每一页上。 印刷器/印记签署器项支持通过多页的图形上传时，此属性很有用 (TYMED\_多页\_文件) 文件格式传输。 此属性已初始化并维护 WIA 微型驱动程序，并且可与 Windows 8 和更高版本的 Windows。

属性类型：VT\_UI4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

**WIA\_IPS\_打印机\_印记签署器\_最大\_图形**属性是可选的支持图形的印刷器/印记签署器项上传。 实现时，属性值**必须是**大于零 (0)。

详细了解 TYMED\_多页\_文件常量，请参阅[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

 

 






