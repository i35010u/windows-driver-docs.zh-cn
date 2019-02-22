---
title: DEVPROP_TYPE_INT32
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT32 标识符表示基本数据类型标识符，该值指示数据类型为 long 类型的值类型的有符号的整数。
ms.assetid: 55a26644-1779-4330-8a45-52b06b634544
keywords:
- DEVPROP_TYPE_INT32 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_INT32
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a669b152c2a3570e9eee86d817a7529b09aa2a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522153"
---
# <a name="devproptypeint32"></a>DEVPROP_TYPE_INT32


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT32 标识符表示基本数据类型标识符，该值指示数据类型为 long 类型的值类型的有符号的整数。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_INT32 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

**设置此属性类型**

若要设置其基本数据类型为 DEVPROP_TYPE_INT32 的属性，调用对应**SetupDiSet * Xxx*** 属性函数，设置函数的输入的参数，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_INT32，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个长整型值，并设置*PropertyBufferSize*参数<strong>sizeof (</strong>长<strong>)</strong>。

- 根据需要设置其他函数输入的参数设置的属性。

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

 

 





