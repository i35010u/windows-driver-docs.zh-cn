---
title: DEVPROP_TYPE_STRING_LIST
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_STRING_LIST 属性类型表示基本数据类型标识符，该值指示数据类型为[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的 Unicode 字符串的类型的列表。
ms.assetid: 91cfba02-cdd4-4918-8fc1-7e7793058074
keywords:
- DEVPROP_TYPE_STRING_LIST 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING_LIST
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee4fe69ccdd80dcc22a8ce0a09f6fb5ef44a3811
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575728"
---
# <a name="devproptypestringlist"></a>DEVPROP_TYPE_STRING_LIST


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_STRING_LIST 属性类型表示基本数据类型标识符，该值指示数据类型为[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的 Unicode 字符串的类型的列表。

<a name="remarks"></a>备注
-------

不能与属性数据类型修饰符组合 DEVPROP_TYPE_STRING_LIST。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_STRING_LIST 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_STRING_LIST，参数设置*PropertyBuffer*指向包含缓冲区的指针参数[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的列表Unicode 字符串，并设置*PropertyBufferSize*参数大小 （字节） 的列表，包括最终列表为 NULL 终止符。

-   根据需要设置其他函数输入的参数设置的属性。

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

 

 





