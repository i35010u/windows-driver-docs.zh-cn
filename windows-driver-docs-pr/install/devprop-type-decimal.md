---
title: DEVPROP_TYPE_DECIMAL
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_INT64 标识符表示数据类型为十进制类型的值的基本数据类型标识符。
keywords:
- DEVPROP_TYPE_DECIMAL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DECIMAL
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4879c1cce35d799b6afe78885504a3373a9195e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813191"
---
# <a name="devprop_type_decimal"></a>DEVPROP_TYPE_DECIMAL


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_INT64 标识符表示数据类型为十进制类型的值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

DEVPROP_TYPE_DECIMAL 只能与 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 的属性数据类型修饰符组合。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其数据类型为 DEVPROP_TYPE_DECIMAL 的属性，请调用相应的 SetupDiSet *Xxx* 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_DECIMAL，将 *PropertyBuffer* 参数设置为指向一个缓冲区的指针，该缓冲区可包含至少一个十进制值，并将 *PropertyBufferSize* 参数设置为 `sizeof(DECIMAL)` 。

-   根据需要设置其他函数输入参数来设置属性。

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

 

 





