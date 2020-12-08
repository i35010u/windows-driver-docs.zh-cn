---
title: DEVPROP_MASK_TYPE
description: 在 Windows Vista 和更高版本的 Windows 中，可以使用按位 "与" 属性数据类型标识符将 DEVPROP_MASK_TYPE 掩码组合在一起，以便从属性数据类型标识符中提取基本数据类型标识符。
keywords:
- DEVPROP_MASK_TYPE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_MASK_TYPE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e95fd1e98d47480a5ebffb9b6df79c5491c0df72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813741"
---
# <a name="devprop_mask_type"></a>DEVPROP_MASK_TYPE


在 Windows Vista 和更高版本的 Windows 中，可以使用按位 "与" [属性数据类型标识符](/previous-versions/ff541476(v=vs.85)) 将 DEVPROP_MASK_TYPE 掩码组合在一起，以便从属性数据类型标识符中提取 [**基本数据类型标识符**](/previous-versions/ff537793(v=vs.85)) 。

<a name="remarks"></a>备注
-------

不能将此掩码用作基本数据类型标识符、属性数据类型修饰符或属性数据类型标识符。

有关如何从属性数据类型标识符提取 DEVPROP_TYPEMOD_Xxx 的 [**属性数据类型修饰符**](/previous-versions/ff549770(v=vs.85)) 的信息，请参阅 [**DEVPROP_MASK_TYPEMOD**](devprop-mask-typemod.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROP_MASK_TYPEMOD**](devprop-mask-typemod.md)

 

