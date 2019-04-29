---
title: DEVPROP_TYPE_CURRENCY
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_CURRENCY 标识符表示指示数据类型为货币类型值的基本数据类型标识符。
ms.assetid: e79d4351-79a0-4e7a-9290-dd02d317a958
keywords:
- DEVPROP_TYPE_CURRENCY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_CURRENCY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 54a92b68383cd388c92989c654f14c9a4500f687
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360629"
---
# <a name="devproptypecurrency"></a>DEVPROP_TYPE_CURRENCY


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_CURRENCY 标识符表示指示数据类型为货币类型值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_CURRENCY [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_CURRENCY 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_CURRENCY，参数设置*PropertyBuffer*参数指向的缓冲区，其中包含一个货币值，并设置*PropertyBufferSize*参数`sizeof(CURRENCY)`。

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

 

 





