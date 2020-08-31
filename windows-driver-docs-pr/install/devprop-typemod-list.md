---
title: DEVPROP_TYPEMOD_LIST
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPEMOD_LIST 标识符表示一个属性数据类型修饰符，该修饰符只能与基本数据类型标识符组合 DEVPROP_TYPE_STRING 和 DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING，以创建表示以 NULL 结尾的 Unicode 字符串的 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 列表的属性数据类型标识符。
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
ms.openlocfilehash: 315855c1a0046406ca0e13b5b9b584b1945d352d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095423"
---
# <a name="devprop_typemod_list"></a>DEVPROP_TYPEMOD_LIST


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPEMOD_LIST 标识符表示一个属性数据类型修饰符，该修饰符只能与[**基本数据类型标识符**](/previous-versions/ff537793(v=vs.85))组合 [**DEVPROP_TYPE_STRING**](devprop-type-string.md)和[**DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING**](devprop-type-security-descriptor-string.md) ，以创建表示以 NULL 结尾的 Unicode 字符串的[REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types)列表的属性数据类型标识符。

<a name="remarks"></a>备注
-------

不能将 DEVPROP_TYPEMOD_LIST 与 [**DEVPROP_TYPE_EMPTY**](devprop-type-empty.md)、 [**DEVPROP_TYPE_NULL**](devprop-type-null.md)、 [**DEVPROP_TYPE_SECURITY_DESCRIPTOR**](devprop-type-security-descriptor.md)或任何固定长度的基本数据类型标识符组合在一起。

若要创建表示字符串列表的属性数据类型标识符，请在 DEVPROP_TYPEMOD_LIST 的属性数据类型修饰符和相应的 DEVPROP_TYPE_Xxx 标识符之间执行按位 "或"。 例如，若要指定 Unicode 字符串 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 列表，请执行以下按位 or： (DEVPROP_TYPEMOD_LIST |DEVPROP_TYPE_STRING) 。

以 NULL 结尾的 Unicode 字符串 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 列表的大小是列表的大小，其中包括终止列表的最终 **NULL** 。

有关如何创建表示固定长度数据值数组的属性数据类型标识符的信息，请参阅 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)。

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


[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

