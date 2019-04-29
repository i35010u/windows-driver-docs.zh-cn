---
title: WIA\_DPC\_PICT\_宽度
description: WIA\_DPC\_PICT\_宽度属性描述的宽度，以像素为单位，用于为新捕获的映像。
ms.assetid: 08ff2ef6-1c65-4a46-bf17-f7c5126279d4
keywords:
- WIA_DPC_PICT_WIDTH 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_PICT_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14e680189e83e12bc284bd30d1b1ee52f67cf157
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379593"
---
# <a name="wiadpcpictwidth"></a>WIA\_DPC\_PICT\_宽度


WIA\_DPC\_PICT\_宽度属性描述的宽度，以像素为单位，用于为新捕获的映像。

## <span id="ddk_wia_dpc_pict_width_si"></span><span id="DDK_WIA_DPC_PICT_WIDTH_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA 的有效值的列表\_DPC\_PICT\_宽度属性具有一对一的对应关系到的有效值列表[ **WIA\_DPC\_PICT\_高度**](wia-dpc-pict-height.md)属性。 如果单个宽度和高度以线性方式可设置和正交到对方，可以将它们表示为一个范围。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPC\_PICT\_HEIGHT**](wia-dpc-pict-height.md)

 

 






