---
title: WIA \_ DPS \_ PAD \_ 颜色
description: WIA \_ DPS \_ PAD \_ COLOR 属性包含 wia 微型驱动程序填充未对齐的数据时使用的当前填充颜色。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPS_PAD_COLOR 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PAD_COLOR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a88b1b1e84bfac3a61678e508416bc6c06f951
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831771"
---
# <a name="wia_dps_pad_color"></a>WIA \_ DPS \_ PAD \_ 颜色


WIA \_ DPS \_ PAD \_ COLOR 属性包含 wia 微型驱动程序填充未对齐的数据时使用的当前填充颜色。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_pad_color_si"></span><span id="DDK_WIA_DPS_PAD_COLOR_SI"></span>


属性类型： VT \_ UI1 |VT \_ 矢量

有效值： WIA " \_ \_ 无"

访问权限：读/写

<a name="remarks"></a>备注
-------

\_应将 "WIA DPS \_ PAD \_ 颜色" 属性报告为四个字节值的向量，格式为 "RGBQUAD 结构 (，如 Microsoft Windows SDK 文档) 中所述。

应用程序将读取 WIA \_ DPS \_ PAD \_ 颜色以获取所使用的填充颜色。

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

 

 





