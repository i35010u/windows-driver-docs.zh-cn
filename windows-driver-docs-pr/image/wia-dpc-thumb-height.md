---
title: WIA\_DPC\_THUMB\_高度
description: WIA\_DPC\_THUMB\_高度属性定义的高度，以像素为单位，缩略图用于新捕获的映像。
ms.assetid: bc4ad063-7287-461e-a31b-d4b6628372b6
keywords:
- WIA_DPC_THUMB_HEIGHT 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_THUMB_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6343cd5da28df70ca5c65163e3ac53d483e298d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392558"
---
# <a name="wiadpcthumbheight"></a>WIA\_DPC\_THUMB\_高度


WIA\_DPC\_THUMB\_高度属性定义的高度，以像素为单位，缩略图用于新捕获的映像。

## <span id="ddk_wia_dpc_thumb_height_si"></span><span id="DDK_WIA_DPC_THUMB_HEIGHT_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE 或 WIA\_PROP\_列表

访问权限：只读或读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPC\_THUMB\_要获取用于在其用户界面中显示缩略图图像的估计的大小的高度值。

如果值或 WIA\_DPC\_THUMB\_高度是 WIA\_PROP\_无、 访问权限必须是只读的。 如果值为 WIA\_PROP\_列表中，访问权限必须是读/写。

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


[**WIA\_DPC\_THUMB\_WIDTH**](wia-dpc-thumb-width.md)

 

 






