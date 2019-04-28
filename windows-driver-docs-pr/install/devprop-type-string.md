---
title: DEVPROP_TYPE_STRING
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_STRING 属性类型表示，该值指示数据类型为以 NULL 结尾的 Unicode 字符串的基本数据类型标识符。
ms.assetid: b578fa1f-b55d-4ad2-bdc4-a796b5d7b811
keywords:
- DEVPROP_TYPE_STRING 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4c835ce41382e712c5c652d823e0f9f5f3bfb2c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331277"
---
# <a name="devproptypestring"></a>DEVPROP_TYPE_STRING


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_STRING 属性类型表示，该值指示数据类型为以 NULL 结尾的 Unicode 字符串的基本数据类型标识符。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_STRING [ **DEVPROP_TYPEMOD_LIST** ](devprop-typemod-list.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_STRING 的属性，调用对应**SetupDiSet * Xxx*** 属性函数，设置函数的输入的参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_STRING，参数设置*PropertyBuffer*参数指向的缓冲区，其中包含以 NULL 结尾的 Unicode 字符串，并设置*PropertyBufferSize*参数大小 （字节） 包括 NULL 终止符的字符串。

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

 

 





