---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ FONT \_ TYPE
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ font \_ type 属性配置 PRINTER/ENDORSER 设备使用的字体类型。
keywords:
- WIA_IPS_PRINTER_ENDORSER_FONT_TYPE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_FONT_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d77224aa2108460a4f44043e5b275ba48250624
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838277"
---
# <a name="wia_ips_printer_endorser_font_type"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ FONT \_ TYPE


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ font \_ type** 属性配置 PRINTER/ENDORSER 设备使用的字体类型。 此属性由 WIA 迷你驱动程序初始化和维护。 此功能适用于 windows 8 和更高版本的 Windows。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限： Read-Write

<a name="remarks"></a>备注
-------

下表显示了 " **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 字体 \_ 类型** " 属性的接受值。

| “值”                                        | 描述                       |
|----------------------------------------------|-----------------------------------|
| WIA \_ 打印 \_ 字体 \_ 正常                     | 普通字体。                      |
| WIA \_ 打印 \_ 字体 \_ 加粗                       | 粗体。                        |
| WIA \_ 打印 \_ 字体 \_ 特大 \_                | 附加粗体字体。                  |
| WIA \_ 打印 \_ 字体 \_ 斜体 \_               | 斜体、粗体。                |
| WIA \_ 打印 \_ 字体 \_ 斜体 \_ 黑体 \_        | 斜体、附加粗体字体。          |
| WIA \_ 打印 \_ 字体 \_ 斜体                     | 斜体字体。                      |
| WIA \_ 打印 \_ 字体 \_ 较小                      | 小号字体。                       |
| WIA \_ 打印 \_ 字体 \_ 小 \_ 粗体                | 小号粗体。                  |
| WIA \_ 打印 \_ 字体 \_ 小 \_ 额外 \_ 粗体         | 较小的额外粗体字体。            |
| WIA \_ 打印 \_ 字体 \_ 小 \_ 斜体 \_        | 小号倾斜和粗体。       |
| WIA \_ 打印 \_ 字体 \_ 小 \_ 斜体 \_ 额外 \_ 粗体 | 小型斜体和额外粗体字体。 |
| WIA \_ 打印 \_ 字体- \_ 小 \_ 斜体              | 小型斜体。                |
| WIA \_ 打印 \_ \_ 大字体                      | 大字体。                       |
| WIA \_ 打印 \_ 字体 \_ 大 \_ 粗体                | 大粗体。                  |
| WIA \_ 打印 \_ 字体 \_ 较大 \_ 额外 \_ 粗体         | 特大额外粗体字。            |
| WIA \_ 打印 \_ 字体 \_ 大 \_ 斜体 \_        | 大斜体和粗体。       |
| WIA \_ 打印 \_ 字体 \_ 大 \_ 斜体 \_ 特 \_ 粗 | 大斜体和额外粗体字。 |
| WIA \_ 打印 \_ 字体 \_ 大 \_ 斜体              | 大斜体字体。                |

 

对于 Imprinter/Endorser 项， **WIA \_ IPS \_ PRINTER \_ ENDORSER \_ FONT \_ TYPE** 属性是可选的。 如果不支持此功能，则 printer/endorser 设备不支持字体配置。

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

 

 





