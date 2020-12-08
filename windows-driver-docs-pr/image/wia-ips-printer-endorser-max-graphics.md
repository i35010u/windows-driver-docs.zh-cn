---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 最大 \_ 图形
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ GRAPHICS 属性介绍了 Imprinter/ENDORSER 项可以在每一页上打印或认可的图像的最大数目。
keywords:
- WIA_IPS_PRINTER_ENDORSER_MAX_GRAPHICS 图像设备
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
ms.openlocfilehash: cf29a996ecc21c1e8809a5cfdd871e213040317e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839529"
---
# <a name="wia_ips_printer_endorser_max_graphics"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 最大 \_ 图形


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ GRAPHICS** 属性介绍了 Imprinter/ENDORSER 项可以在每一页上打印或认可的图像的最大数目。 当 Imprinter/Endorser 项支持通过多页 (TYMED 多页文件进行图形上传 \_ \_) 文件格式传输时，此属性很有用。 此属性由 WIA 迷你驱动程序初始化和维护，并且在 Windows 8 及更高版本的 Windows 中可用。

属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

对于支持图形上传的 Imprinter/Endorser 项， **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ MAX \_ GRAPHICS** 属性是可选的。 实现时，属性值 **必须** 大于零 (0) 。

有关 TYMED \_ 多页文件常量的详细信息 \_ ，请参阅 [**WIA \_ IPA \_ TYMED**](wia-ipa-tymed.md)。

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


[**WIA \_ IPA \_ TYMED**](wia-ipa-tymed.md)

 

 






