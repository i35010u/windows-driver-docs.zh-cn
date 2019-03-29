---
title: WIA\_DPC\_图片\_剩余
description: WIA\_DPC\_图片\_剩余属性包含的用户可以使用摄像机设备，给定的当前属性设置拍摄的照片的数量。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: ac6cd3e0-c6fe-4783-8094-67083e308308
keywords:
- WIA_DPC_PICTURES_REMAINING 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_PICTURES_REMAINING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92dc180099c5f358bc1ae852b31c8b4ebd9cbf31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562490"
---
# <a name="wiadpcpicturesremaining"></a>WIA\_DPC\_图片\_剩余


WIA\_DPC\_图片\_剩余属性包含的用户可以使用摄像机设备，给定的当前属性设置拍摄的照片的数量。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpc_pictures_remaining_si"></span><span id="DDK_WIA_DPC_PICTURES_REMAINING_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果 WIA\_DPC\_图片\_剩余属性设置更改和所做的更改会影响照相机设备生成的图像的大小，应将 WIA 微型驱动程序更新的剩余的照片的数量。

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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





