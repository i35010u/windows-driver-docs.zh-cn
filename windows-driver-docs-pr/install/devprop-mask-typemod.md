---
title: DEVPROP_MASK_TYPEMOD
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_MASK_TYPEMOD 掩码可以在按位 "与" 属性数据类型标识符组合在一起，以便从属性数据类型标识符提取 DEVPROP_TYPEMOD_Xxx 的属性数据类型修饰符。
ms.assetid: 9ed153d7-dd37-4978-9e03-44efac2ab97a
keywords:
- DEVPROP_MASK_TYPEMOD 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_MASK_TYPEMOD
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 300415646e2f9023baf5156676e1d09d90b16e0a
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095923"
---
# <a name="devprop_mask_typemod"></a>DEVPROP_MASK_TYPEMOD


在 Windows Vista 和更高版本的 Windows 中，可以在按位 "与" 的 [属性数据类型标识符](/previous-versions/ff541476(v=vs.85)) 中组合 DEVPROP_MASK_TYPEMOD 掩码，以便从属性数据类型标识符提取 DEVPROP_TYPEMOD_*Xxx* [**属性数据类型修饰符**](/previous-versions/ff549770(v=vs.85)) 。

<a name="remarks"></a>备注
-------

不能将此掩码用作基本数据类型标识符、属性数据类型修饰符或属性数据类型标识符。

有关如何从属性数据类型标识符提取 [**基本数据类型标识符**](/previous-versions/ff537793(v=vs.85)) 的信息，请参阅 [**DEVPROP_MASK_TYPE**](devprop-mask-type.md)。

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

## <a name="see-also"></a>另请参阅


[**DEVPROP_MASK_TYPE**](devprop-mask-type.md)

 

