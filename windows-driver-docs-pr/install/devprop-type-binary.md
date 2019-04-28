---
title: DEVPROP_TYPE_BINARY
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BINARY 标识符表示基本数据类型标识符，该值指示数据类型为 BYTE 类型无符号值的数组。
ms.assetid: ee20f0f1-fff9-41a9-a880-f8f577320e41
keywords:
- DEVPROP_TYPE_BINARY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BINARY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aca3498dc91865e6bf8a8d2a5c0114879b494eb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327474"
---
# <a name="devproptypebinary"></a>DEVPROP_TYPE_BINARY


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_BINARY 标识符表示基本数据类型标识符，该值指示数据类型为 BYTE 类型无符号值的数组。

<a name="remarks"></a>备注
-------

不能与属性数据类型修饰符组合 DEVPROP_TYPE_BINARY 属性类型。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_BINARY 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_BINARY，参数设置*PropertyBuffer*指向包含的字节值，并设置数组的缓冲区的指针参数*PropertyBufferSize*参数的大小，以字节为单位的缓冲区。

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

 

 





