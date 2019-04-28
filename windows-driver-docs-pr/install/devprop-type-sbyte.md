---
title: DEVPROP_TYPE_SBYTE
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BYTE 标识符表示指示数据类型是 SBYTE 类型有符号的整数的基本数据类型标识符。
ms.assetid: d2c503aa-4427-4745-b3c2-57b6ebd0e93c
keywords:
- DEVPROP_TYPE_SBYTE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SBYTE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9f9af4a4eea1d661d99ab0593f1f5edb56aa891
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344309"
---
# <a name="devproptypesbyte"></a>DEVPROP_TYPE_SBYTE


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BYTE 标识符表示指示数据类型是 SBYTE 类型有符号的整数的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_SBYTE [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

**设置此属性类型**

若要设置其数据类型为 DEVPROP_TYPE_BYTE 的属性，调用对应**SetupDiSet * Xxx*** 属性函数，并将函数参数设置，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_BYTE，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个字节值，并设置*PropertyBufferSize*参数<strong>sizeof (</strong>字节<strong>)</strong>。

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
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

 

 





