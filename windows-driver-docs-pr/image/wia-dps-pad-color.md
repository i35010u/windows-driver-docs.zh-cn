---
title: WIA\_DPS\_PAD\_颜色
description: WIA\_DPS\_PAD\_颜色属性包含当前 WIA 微型驱动程序来填充未对齐的数据时使用的填充颜色。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: db78fc1b-72e4-4edc-8f4f-9209e6b36aa6
keywords:
- WIA_DPS_PAD_COLOR 成像设备
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
ms.openlocfilehash: 45da42ad8c6d7d70794a31c49e9d3ea44d79beca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554543"
---
# <a name="wiadpspadcolor"></a>WIA\_DPS\_PAD\_颜色


WIA\_DPS\_PAD\_颜色属性包含当前 WIA 微型驱动程序来填充未对齐的数据时使用的填充颜色。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_pad_color_si"></span><span id="DDK_WIA_DPS_PAD_COLOR_SI"></span>


属性类型：VT\_UI1 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPS\_PAD\_COLOR 属性应报告为 RGBQUAD 结构 （它 Microsoft Windows SDK 文档中所述） 的窗体中的 4 字节值的向量。

应用程序读取 WIA\_DPS\_PAD\_颜色以获取所使用的填充颜色。

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

 

 





