---
title: WIA\_DPC\_PICT\_高度
description: WIA\_DPC\_PICT\_高度属性包含的高度，以像素为单位，用于为新捕获的映像。
ms.assetid: 07320fa4-ef21-4cda-9fc0-fe788f653c31
keywords:
- WIA_DPC_PICT_HEIGHT 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_PICT_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a7b838bb9a7a21ea1ec413ab073f4a42f2323d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524503"
---
# <a name="wiadpcpictheight"></a>WIA\_DPC\_PICT\_高度


WIA\_DPC\_PICT\_高度属性包含的高度，以像素为单位，用于为新捕获的映像。

## <span id="ddk_wia_dpc_pict_height_si"></span><span id="DDK_WIA_DPC_PICT_HEIGHT_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA 的有效值的列表\_DPC\_PICT\_高度属性具有一对一的对应关系的有效值列表[ **WIA\_DPC\_PICT\_宽度**](wia-dpc-pict-width.md)属性。 如果单个宽度和高度以线性方式可设置和正交到对方，可以将它们表示为一个范围。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPC\_PICT\_WIDTH**](wia-dpc-pict-width.md)

 

 






