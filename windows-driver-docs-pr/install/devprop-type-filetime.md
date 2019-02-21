---
title: DEVPROP_TYPE_FILETIME
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_FILETIME 属性类型表示指示数据类型为 FILETIME 类型化值的基本数据类型标识符。
ms.assetid: e81585ae-ee47-456b-b29b-24217fab5f9a
keywords:
- DEVPROP_TYPE_FILETIME 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_FILETIME
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b18b9cb7afb3f2bda4a519dbe26c5f49bddd3349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545795"
---
# <a name="devproptypefiletime"></a>DEVPROP_TYPE_FILETIME


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_FILETIME 属性类型表示指示数据类型为 FILETIME 类型化值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

我们建议，以协调世界时 (UTC) 为单位表示所有时间值。

可以仅与组合 DEVPROP_TYPE_FILETIME [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_FILETIME 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_DATE，参数设置*PropertyBuffer*指向包含 FILETIME 结构的缓冲区的指针参数和设置*PropertyBufferSize*参数`sizeof(FILETIME)`。

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

 

 





