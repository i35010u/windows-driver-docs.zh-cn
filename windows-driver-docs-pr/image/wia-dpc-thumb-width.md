---
title: WIA \_ DPC \_ 拇指 \_ 宽度
description: WIA \_ DPC \_ 拇指 \_ WIDTH 属性定义用于新捕获图像的缩略图的宽度（以像素为单位）。
keywords:
- WIA_DPC_THUMB_WIDTH 图像设备
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
ms.openlocfilehash: 82aa9f7601f0356a3dc89b9e5b43b9ee5d22b994
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802441"
---
# <a name="wia_dpc_thumb_width"></a>WIA \_ DPC \_ 拇指 \_ 宽度


WIA \_ DPC \_ 拇指 \_ WIDTH 属性定义用于新捕获图像的缩略图的宽度（以像素为单位）。

## <span id="ddk_wia_dpc_thumb_width_si"></span><span id="DDK_WIA_DPC_THUMB_WIDTH_SI"></span>


属性类型： VT \_ I4

有效值： WIA \_ \_ "无" 或 "wia"。 \_ \_

访问权限：只读或读/写

<a name="remarks"></a>备注
-------

应用程序将读取 WIA \_ DPC \_ 拇指 \_ WIDTH 值，以获取在其用户界面中显示缩略图图像的估计大小。

如果值或 WIA \_ DPC \_ 拇指 \_ 宽度为 WIA \_ \_ "无"，则访问权限必须为只读。 如果值为 WIA 目录 \_ \_ 列表，则访问权限必须是读/写。

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
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ 拇指 \_ 高度**](wia-dpc-thumb-height.md)

 

 






