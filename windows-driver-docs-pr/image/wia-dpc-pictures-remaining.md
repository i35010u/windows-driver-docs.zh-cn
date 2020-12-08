---
title: 保留的 WIA \_ DPC \_ 图片 \_
description: 如果 \_ \_ 当前的属性设置为，则 WIA DPC PICTURES " \_ 属性" 包含用户使用照相机设备可以执行的图片数。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPC_PICTURES_REMAINING 图像设备
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
ms.openlocfilehash: 2f8ad287cec3ef6373658d8aa3a0164b7b26b77d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791491"
---
# <a name="wia_dpc_pictures_remaining"></a>保留的 WIA \_ DPC \_ 图片 \_


如果 \_ \_ 当前的属性设置为，则 WIA DPC PICTURES " \_ 属性" 包含用户使用照相机设备可以执行的图片数。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpc_pictures_remaining_si"></span><span id="DDK_WIA_DPC_PICTURES_REMAINING_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果 WIA \_ DPC \_ 图片 " \_ 剩余" 属性设置发生更改，并且更改影响照相机设备产生的图像大小，则 WIA 微型驱动程序应更新剩余图片的数目。

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

 

 





