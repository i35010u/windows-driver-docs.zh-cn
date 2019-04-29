---
title: DEVPROP_TYPE_DEVPROPTYPE
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DEVPROPTYPE 标识符表示指示数据类型为 DEVPROPTYPE 类型化值的基本数据类型标识符。
ms.assetid: d50a26d4-0af5-4cc5-aaa4-8587b64fc1a8
keywords:
- DEVPROP_TYPE_DEVPROPTYPE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DEVPROPTYPE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6ba4d0c9147a772a546a4a28a25ff018a1832a6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357773"
---
# <a name="devproptypedevproptype"></a>DEVPROP_TYPE_DEVPROPTYPE


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DEVPROPTYPE 标识符表示指示数据类型为 DEVPROPTYPE 类型化值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_DEVPROPTYPE 属性类型[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_DEVPROPTYPE 的属性，调用相应 SetupDiSet*Xxx*属性函数，设置函数的输入的参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_DEVPROPTYPE，参数设置*PropertyBuffer*参数指向的缓冲区包含 DEVPROPTYPE 值，并设置*PropertyBufferSize*参数`sizeof(DEVPROPTYPE)`。

-   根据需要设置剩余函数参数设置的属性。

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

 

 





