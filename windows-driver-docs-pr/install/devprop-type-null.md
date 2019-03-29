---
title: DEVPROP_TYPE_NULL
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_NULL 标识符表示特殊的基本数据类型标识符，以指示设备属性存在。 但是，属性的值与该键相关联的属性。
ms.assetid: 0308206d-5664-4288-a761-ca72e533264c
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
ms.openlocfilehash: f5ba1bdac9df8044d91126266a65172fb7e2922d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562008"
---
# <a name="devproptypenull"></a>DEVPROP_TYPE_NULL


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_NULL 标识符表示特殊的基本数据类型标识符，以指示设备属性存在。 但是，属性的值与该键相关联的属性。

<a name="remarks"></a>备注
-------

使用此属性的基本类型标识符的设备属性函数删除与设备属性关联的值。

如果设备属性函数返回此基本数据类型，该属性存在，但属性没有任何与之相关联的值。

不能与属性数据类型修饰符组合 DEVPROP_TYPE_NULL 标识符[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)或[ **DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md).

**设置此属性类型**

若要设置其数据类型为 DEVPROP_TYPE_NULL 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集作为函数参数后面：

-   设置*PropertyType* DEVPROP_TYPE_NULL，参数*PropertyBuffer*参数**NULL**，以及*PropertyBufferSize*参数为零。

-   根据需要设置其他函数输入的参数设置的属性。

**检索此类型的属性**

调用**SetupDiGet * Xxx*** 尝试检索没有值的设备属性的属性函数将会胜出并设置\* *PropertyType* DEVPROP_TYPE_NULL 参数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

 

 





