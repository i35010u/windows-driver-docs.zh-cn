---
title: DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 标识符表示指示数据类型是一个以 NULL 结尾的 Unicode 字符串，包含安全描述符中的基本数据类型标识符安全描述符定义语言 (SDDL) 格式。
ms.assetid: 2d791816-bb0e-4275-953f-1492886e9545
keywords:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: df63ac424df81aff23a53206fd340b702858bf02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520291"
---
# <a name="devproptypesecuritydescriptorstring"></a>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 标识符表示指示数据类型是一个以 NULL 结尾的 Unicode 字符串，包含安全描述符中的基本数据类型标识符安全描述符定义语言 (SDDL) 格式。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING [ **DEVPROP_TYPEMOD_LIST** ](devprop-typemod-list.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING，参数设置*PropertyBuffer*指向包含以 NULL 结尾的安全描述符字符串的缓冲区的指针参数并设置*PropertyBufferSize*大小 （字节） 包括 NULL 终止符的安全描述符字符串参数。

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
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

 

 





