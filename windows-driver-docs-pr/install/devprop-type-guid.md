---
title: DEVPROP_TYPE_GUID
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_GUID 标识符表示基本数据类型标识符，以指示数据类型的 GUID 类型的全局唯一标识符 (GUID)。
ms.assetid: 77080860-c2b3-4c7c-8ab8-e0b02582ffbb
keywords:
- DEVPROP_TYPE_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_GUID
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 07c3280dc99818f75223af4d6ef7415093b84933
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568062"
---
# <a name="devproptypeguid"></a>DEVPROP_TYPE_GUID


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_GUID 标识符表示基本数据类型标识符，以指示数据类型的 GUID 类型的全局唯一标识符 (GUID)。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_GUID [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_GUID 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_GUID，参数设置*PropertyBuffer*参数指向的缓冲区包含 GUID 值，并设置*PropertyBufferSize*参数`sizeof(GUID)`。

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

 

 





