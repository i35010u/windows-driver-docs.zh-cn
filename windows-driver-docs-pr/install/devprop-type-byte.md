---
title: DEVPROP_TYPE_BYTE
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BYTE 标识符表示指示数据类型是字节类型的无符号的整数的基本数据类型标识符。
ms.assetid: cda681f0-948d-4534-bf56-2ad9dd8a845c
keywords:
- DEVPROP_TYPE_BYTE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BYTE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f51f32856d6c6c646ab4a5c0dcd96bb9d03c4fee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327439"
---
# <a name="devproptypebyte"></a>DEVPROP_TYPE_BYTE


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BYTE 标识符表示指示数据类型是字节类型的无符号的整数的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_BYTE [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其数据类型为 DEVPROP_TYPE_BYTE 的属性，调用相应 SetupDiSet*Xxx*属性函数，设置函数的输入的参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_BYTE，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个字节值，并设置*PropertyBufferSize*参数`sizeof(BYTE)`。

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

 

 





