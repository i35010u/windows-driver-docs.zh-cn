---
title: DEVPROP_TYPE_STRING
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_STRING 属性类型表示数据类型为 NULL 终止的 Unicode 字符串的基本数据类型标识符。
keywords:
- DEVPROP_TYPE_STRING 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a81442be25d5b6a9ce4a3c5eae8c500611a44b5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791467"
---
# <a name="devprop_type_string"></a>DEVPROP_TYPE_STRING


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_STRING 属性类型表示数据类型为 NULL 终止的 Unicode 字符串的基本数据类型标识符。

<a name="remarks"></a>备注
-------

DEVPROP_TYPE_STRING 只能与 [**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md) 的属性数据类型修饰符组合。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_STRING 的属性，请调用相应的 **SetupDiSet * Xxx*** 属性函数，并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_STRING，将 *PropertyBuffer* 参数设置为指向包含以 NULL 结尾的 Unicode 字符串的缓冲区的指针，并将 *PropertyBufferSize* 参数设置为字符串的大小（以字节为单位），包括 null 终止符。

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

 

 





