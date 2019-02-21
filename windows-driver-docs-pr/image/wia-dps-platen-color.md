---
title: WIA\_DPS\_辊\_颜色
description: WIA\_DPS\_辊\_颜色属性包含当前辊颜色。
ms.assetid: d1bc9bc8-ad23-48b8-8456-21aa3556ab69
keywords:
- WIA_DPS_PLATEN_COLOR 成像设备
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
ms.openlocfilehash: 613b8448d2b5364a4c0059256ab49165b573f68d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555667"
---
# <a name="wiadpsplatencolor"></a>WIA\_DPS\_辊\_颜色


WIA\_DPS\_辊\_颜色属性包含当前辊颜色。

## <span id="ddk_wia_dps_platen_color_si"></span><span id="DDK_WIA_DPS_PLATEN_COLOR_SI"></span>


属性类型：VT\_UI1 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

微型驱动程序应报告 WIA\_DPS\_辊\_颜色为 RGBQUAD 结构 （它 Microsoft Windows SDK 文档中所述） 的窗体中的 4 字节值的向量。 WIA 微型驱动程序创建并维护此属性。

应用程序读取 WIA\_DPS\_辊\_获取扫描程序的辊颜色的颜色。 此颜色可帮助应用程序后期处理最终映像。

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

 

 





