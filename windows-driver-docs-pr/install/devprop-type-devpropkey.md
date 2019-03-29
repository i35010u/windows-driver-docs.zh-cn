---
title: DEVPROP_TYPE_DEVPROPKEY
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DEVPROPKEY 标识符表示指示数据类型为 DEVPROPKEY 类型设备属性键的基本数据类型标识符。
ms.assetid: 4b0f0f33-9a9e-498a-b2f3-e215bac68dd9
keywords:
- DEVPROP_TYPE_DEVPROPKEY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DEVPROPKEY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 348cab367d2199aeefcc7b6459a97a673d0f61a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577184"
---
# <a name="devproptypedevpropkey"></a>DEVPROP_TYPE_DEVPROPKEY


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DEVPROPKEY 标识符表示指示数据类型为 DEVPROPKEY 类型设备属性键的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_DEVPROPKEY 属性类型[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_DEVPROPKEY 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_DEVPROPKEY，参数设置*PropertyBuffer*参数指向的缓冲区包含的 DEVPROPKEY 结构，并设置*PropertyBufferSize*参数`sizeof(DEVPROPKEY)`。

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

 

 





