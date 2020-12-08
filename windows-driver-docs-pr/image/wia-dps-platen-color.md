---
title: WIA \_ DPS \_ 影印 \_ 颜色
description: WIA \_ DPS \_ 影印 \_ 颜色属性包含当前影印颜色。
keywords:
- WIA_DPS_PLATEN_COLOR 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PLATEN_COLOR
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14a2bb8c021dbc8b7da629790e3b1e7f1dc5d471
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831749"
---
# <a name="wia_dps_platen_color"></a>WIA \_ DPS \_ 影印 \_ 颜色


WIA \_ DPS \_ 影印 \_ 颜色属性包含当前影印颜色。

## <span id="ddk_wia_dps_platen_color_si"></span><span id="DDK_WIA_DPS_PLATEN_COLOR_SI"></span>


属性类型： VT \_ UI1 |VT \_ 矢量

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

微型驱动程序应将 WIA \_ DPS \_ 影印颜色报告 \_ 为四个字节值的向量，其形式为 RGBQUAD 结构 (，如 Microsoft Windows SDK 文档) 中所述。 WIA 微型驱动程序创建并维护此属性。

应用程序将读取 WIA \_ DPS \_ 影印 \_ 颜色，以获取扫描仪的影印颜色。 此颜色可帮助应用程序后处理最终映像。

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

 

 





