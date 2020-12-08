---
title: DEVPROP_TYPE_NULL
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_NULL 标识符表示一个特殊的基本数据类型标识符，该标识符指示存在设备属性。 但是，该属性没有与属性关联的值。
keywords:
- DEVPROP_TYPE_NULL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_NULL
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f52d018ea1ad4f06ed79225416d7ed8c594e006
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815347"
---
# <a name="devprop_type_null"></a>DEVPROP_TYPE_NULL


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_NULL 标识符表示一个特殊的基本数据类型标识符，该标识符指示存在设备属性。 但是，该属性没有与属性关联的值。

<a name="remarks"></a>备注
-------

将此基属性类型标识符与设备属性函数结合使用，以删除与设备属性相关联的值。

如果设备属性函数返回此基本数据类型，则属性存在，但该属性没有与之相关联的值。

DEVPROP_TYPE_NULL 标识符不能与属性数据类型修饰符组合 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 或 [**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md)。

**设置此类型的属性**

若要设置其数据类型为 DEVPROP_TYPE_NULL 的属性，请调用相应的 **SetupDiSet * Xxx*** 属性函数并按如下所示设置函数参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_NULL，将 *PropertyBuffer* 参数设置为 **NULL**，将 *PropertyBufferSize* 参数设置为零。

-   根据需要设置其他函数输入参数来设置属性。

**检索此类型的属性**

调用 **SetupDiGet * Xxx*** 属性函数（该函数尝试检索没有值的设备属性），并将 \* *PropertyType* 参数设置为 DEVPROP_TYPE_NULL。

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

 

 





