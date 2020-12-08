---
title: DEVPROP_TYPE_CURRENCY
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_CURRENCY 标识符表示数据类型为货币类型的值的基本数据类型标识符。
keywords:
- DEVPROP_TYPE_CURRENCY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_CURRENCY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5659141a6fb50b4c02c5ff42b8f490594f08d99c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799513"
---
# <a name="devprop_type_currency"></a>DEVPROP_TYPE_CURRENCY


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_CURRENCY 标识符表示数据类型为货币类型的值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

DEVPROP_TYPE_CURRENCY 只能与 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 的属性数据类型修饰符组合。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_CURRENCY 的属性，请调用相应的 SetupDiSet *Xxx* 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_CURRENCY，将 *PropertyBuffer* 参数设置为指向包含货币值的缓冲区的指针，并将 *PropertyBufferSize* 参数设置为 `sizeof(CURRENCY)` 。

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

 

 





