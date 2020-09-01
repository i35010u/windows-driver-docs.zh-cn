---
title: DEVPROP_TYPEMOD_ARRAY
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPEMOD_ARRAY 标识符表示可以与基本数据类型标识符组合在一起的属性数据类型修饰符，以创建表示一组基本数据类型值的属性数据类型标识符。
ms.assetid: 33f12b66-c81a-451b-851a-b58a34a8fe9e
keywords:
- DEVPROP_TYPEMOD_ARRAY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPEMOD_ARRAY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a242debe964da7f0584f6fb445e62350a2e276dc
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097373"
---
# <a name="devprop_typemod_array"></a>DEVPROP_TYPEMOD_ARRAY


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPEMOD_ARRAY 标识符表示可以与 [**基本数据类型标识符**](/previous-versions/ff537793(v=vs.85)) 组合在一起的属性数据类型修饰符，以创建表示一组基本数据类型值的属性数据类型标识符。

<a name="remarks"></a>备注
-------

DEVPROP_TYPEMOD_ARRAY 标识符只能与与数据关联 ([**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85)) 值) 的固定长度的基本数据类型标识符组合在一起。 不能将 DEVPROP_TYPEMOD_ARRAY 标识符与 [**DEVPROP_TYPE_EMPTY**](devprop-type-empty.md)、 [**DEVPROP_TYPE_NULL**](devprop-type-null.md)或任何可变长度的基本数据类型标识符组合在一起。

若要创建表示一组基本数据类型值的属性数据类型标识符，请在 DEVPROP_TYPEMOD_ARRAY 与相应的 DEVPROP_TYPE_*Xxx* 标识符之间执行 "位或" 运算。 例如，若要指定一个无符号字节数组，请执行按位 "或"： (DEVPROP_TYPEMOD_ARRAY | [**DEVPROP_TYPE_BYTE**](devprop-type-byte.md)) 。

基本数据类型值数组的大小（以字节为单位）是数组的大小（以字节为单位）。

有关如何创建表示以 NULL 结尾的 Unicode 字符串 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 列表的属性数据类型标识符的信息，请参阅 [**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md)。

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


[**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))

[**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md)

 

