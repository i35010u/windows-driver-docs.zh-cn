---
title: DEVPROP_TYPE_BOOLEAN
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BOOLEAN 属性类型表示，该值指示数据类型为 DEVPROP_BOOLEAN 类型的布尔值的基本数据类型标识符。
ms.assetid: f0e960b7-be71-4117-b978-5877e5bf771f
keywords:
- DEVPROP_TYPE_BOOLEAN 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BOOLEAN
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 645593588841c0d10157cacc7e64f4f5328846b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327481"
---
# <a name="devproptypeboolean"></a>DEVPROP_TYPE_BOOLEAN


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BOOLEAN 属性类型表示，该值指示数据类型为 DEVPROP_BOOLEAN 类型的布尔值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

按如下所示定义 DEVPROP_BOOLEAN 数据类型和有效的布尔值：

``` syntax
typedef CHAR DEVPROP_BOOLEAN, *PDEVPROP_BOOLEAN;
#define DEVPROP_TRUE  ((DEVPROP_BOOLEAN)-1)
#define DEVPROP_FALSE ((DEVPROP_BOOLEAN) 0)
```

可以仅与组合 DEVPROP_TYPE_BOOLEAN [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_BOOLEAN 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_BOOLEAN，参数设置*PropertyBuffer*指向包含 DEVPROP_FALSE 或 DEVPROP_TRUE 值，缓冲区的指针参数和设置*PropertyBufferSize*参数`sizeof(DEVPROP_BOOLEAN)`。

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

 

 





