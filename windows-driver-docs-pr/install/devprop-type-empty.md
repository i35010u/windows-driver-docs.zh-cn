---
title: DEVPROP_TYPE_EMPTY
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_EMPTY 标识符表示一个指示属性不存在的特殊基本数据类型标识符。
ms.assetid: 23d48659-e512-4557-a78b-d3afca7020a3
keywords:
- DEVPROP_TYPE_EMPTY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_EMPTY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0defffbc2d4077efcefdbb95695610d0e92155d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335241"
---
# <a name="devproptypeempty"></a>DEVPROP_TYPE_EMPTY


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_EMPTY 标识符表示一个指示属性不存在的特殊基本数据类型标识符。

<a name="remarks"></a>备注
-------

使用此基本数据类型标识符的设备属性函数删除属性。

如果设备属性函数返回此基本数据类型标识符，该属性不存在。

**DEVPROP_TYPE_EMPTY**不能与属性数据类型修饰符组合[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)或[ **DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md).

### <a name="deleting-a-property"></a>删除属性

若要删除的属性，调用相应 SetupDiSet*Xxx*属性函数和集作为函数参数后面：

-   设置*PropertyType* DEVPROP_TYPE_EMPTY，参数*PropertyBuffer*参数**NULL**，和*PropertyBufferSize*参数为零。

-   根据需要设置其他函数输入的参数设置的属性。

如果 DEVPROP_TYPE_EMPTY 尝试用于删除不存在的属性，则删除操作将失败，并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回 ERROR_NOT_FOUND。

### <a name="retrieving-a-property-that-does-not-exist"></a>检索一个属性，它不存在

调用 SetupDiGet*Xxx*尝试的检索不存在的设备属性将失败，并随后调用的属性函数[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回 ERROR_NOT_FOUND。 调用的 SetupAPI 属性函数将设置\* *PropertyType* DEVPROP_TYPE_EMPTY 参数。

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

 

 





