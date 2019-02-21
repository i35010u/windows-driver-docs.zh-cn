---
title: DEVPROP_TYPE_UINT32
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_UINT32 标识符表示基本数据类型标识符，该值指示数据类型为 ULONG 类型无符号的整数。
ms.assetid: 671474dd-66be-4c35-8f1a-273f61c6343c
keywords:
- DEVPROP_TYPE_UINT32 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_UINT32
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c3d8ab2909ed84c4bbb438712c3efb837421489a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542306"
---
# <a name="devproptypeuint32"></a>DEVPROP_TYPE_UINT32


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_UINT32 标识符表示基本数据类型标识符，该值指示数据类型为 ULONG 类型无符号的整数。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_UINT32 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

**设置此属性类型**

若要设置其基本数据类型为 DEVPROP_TYPE_UINT32 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_UINT32，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个 ULONG 值，并设置*PropertyBufferSize*参数<strong>sizeof (</strong>ULONG<strong>)</strong>。

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

 

 





