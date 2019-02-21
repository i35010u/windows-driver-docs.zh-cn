---
title: DEVPROP_TYPE_DATE
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DATE 属性类型表示基本数据类型标识符，该值指示数据类型为双精度类型值，该值指定自 1899 年 12 月 31 日以来的天数。
ms.assetid: 0314e7da-d1da-4989-b2cd-90a51c3c8938
keywords:
- DEVPROP_TYPE_DATE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DATE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 55d17d6ca3d644ff7f57683d18a2b3ec23fe9f41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555544"
---
# <a name="devproptypedate"></a>DEVPROP_TYPE_DATE


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_DATE 属性类型表示基本数据类型标识符，该值指示数据类型为双精度类型值，该值指定自 1899 年 12 月 31 日以来的天数。 例如，1900 年 1 月 1 日是 1.0;1900 年 1 月 2 日是 2.0;等等。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_DATE [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_DATE 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_DATE，参数设置*PropertyBuffer*参数指向的缓冲区包含日期值，并设置*PropertyBufferSize*参数`sizeof(DATE)`。

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

 

 





