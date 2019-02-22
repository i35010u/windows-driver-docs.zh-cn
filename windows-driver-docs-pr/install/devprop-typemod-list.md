---
title: DEVPROP_TYPEMOD_LIST
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPEMOD_LIST 标识符表示属性数据类型修饰符，可以只使用基本数据类型标识符 DEVPROP_TYPE_STRING 和 DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 组合若要创建一个表示属性数据类型标识符[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的以 NULL 结尾的 Unicode 字符串列表。
ms.assetid: 0beaa778-55c9-45ac-8163-91d82794a845
keywords:
- DEVPROP_TYPEMOD_LIST 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPEMOD_LIST
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 09215fa94fb7d05caf7c0dd393b3679a42fb05c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521601"
---
# <a name="devproptypemodlist"></a>DEVPROP_TYPEMOD_LIST


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPEMOD_LIST 标识符表示属性数据类型修饰符，可以仅使用组合[**基本数据类型标识符**](https://msdn.microsoft.com/library/windows/hardware/ff537793)  [**DEVPROP_TYPE_STRING** ](devprop-type-string.md)并[ **DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING** ](devprop-type-security-descriptor-string.md)到创建的属性数据类型标识符表示[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的以 NULL 结尾的 Unicode 字符串列表。

<a name="remarks"></a>备注
-------

不能与组合 DEVPROP_TYPEMOD_LIST [ **DEVPROP_TYPE_EMPTY**](devprop-type-empty.md)， [ **DEVPROP_TYPE_NULL**](devprop-type-null.md)， [ **DEVPROP_TYPE_SECURITY_DESCRIPTOR**](devprop-type-security-descriptor.md)，或任何固定的长度数据的基本类型标识符。

若要创建一个表示字符串列表的属性数据类型标识符，请执行 DEVPROP_TYPEMOD_LIST 属性数据类型修饰符和相应的 DEVPROP_TYPE_Xxx 标识符之间的按位 OR。 例如，若要指定[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)列表的 Unicode 字符串，执行以下的按位 OR:(DEVPROP_TYPEMOD_LIST |DEVPROP_TYPE_STRING)。

大小[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的以 NULL 结尾的 Unicode 字符串列表是列表包括最后的大小**NULL**终止列表。

有关如何创建一个表示固定的长度数据值的数组的属性数据类型标识符的信息，请参阅[ **DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)。

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
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






