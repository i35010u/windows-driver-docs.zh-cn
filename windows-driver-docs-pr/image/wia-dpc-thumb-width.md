---
title: WIA\_DPC\_THUMB\_宽度
description: WIA\_DPC\_THUMB\_宽度属性定义的宽度，以像素为单位，缩略图用于新捕获的映像。
ms.assetid: 01136695-9bef-4d47-89df-fb1d14465bef
keywords:
- WIA_DPC_THUMB_WIDTH 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_THUMB_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4278fc0413aa89186e43482d2c6684b40bea25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519623"
---
# <a name="wiadpcthumbwidth"></a>WIA\_DPC\_THUMB\_宽度


WIA\_DPC\_THUMB\_宽度属性定义的宽度，以像素为单位，缩略图用于新捕获的映像。

## <span id="ddk_wia_dpc_thumb_width_si"></span><span id="DDK_WIA_DPC_THUMB_WIDTH_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE，或 WIA\_PROP\_列表

访问权限：只读或读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPC\_THUMB\_要获取用于在其用户界面中显示缩略图图像的估计的大小的宽度值。

如果值或 WIA\_DPC\_THUMB\_宽度是 WIA\_PROP\_无、 访问权限必须是只读的。 如果值为 WIA\_PROP\_列表中，访问权限必须是读/写。

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


[**WIA\_DPC\_THUMB\_HEIGHT**](wia-dpc-thumb-height.md)

 

 






