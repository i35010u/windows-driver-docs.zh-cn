---
title: DEVPROP_TYPE_INT16
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT16 标识符表示指示数据类型是一个短类型的有符号的整数的基本数据类型标识符。
ms.assetid: a126a7c2-744e-4eaf-9b3d-45bd4286de73
keywords:
- DEVPROP_TYPE_INT16 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_INT16
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: df7761f863def61a267639df0d5fe7fd39912293
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533933"
---
# <a name="devproptypeint16"></a>DEVPROP_TYPE_INT16


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT16 标识符表示指示数据类型是一个短类型的有符号的整数的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_SHORT [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

**设置此属性类型**

若要设置其基本数据类型为 DEVPROP_TYPE_INT16 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_INT16，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个短整型值，并设置*PropertyBufferSize*参数<strong>sizeof (</strong>短<strong>)</strong>。

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

 

 





