---
title: DEVPROP_TYPE_SECURITY_DESCRIPTOR
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_SECURITY_DESCRIPTOR 标识符表示指示数据类型为长度可变的自相关，SECURITY_DESCRIPTOR 类型化的安全描述符的基本数据类型标识符。
ms.assetid: e8eea343-adaa-41b8-9556-962b5e6903fb
keywords:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 089675e82ef432740f842184f9c6c12d8cb268db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575849"
---
# <a name="devproptypesecuritydescriptor"></a>DEVPROP_TYPE_SECURITY_DESCRIPTOR


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_SECURITY_DESCRIPTOR 标识符表示指示数据类型为长度可变的自相关，SECURITY_DESCRIPTOR 类型化的安全描述符的基本数据类型标识符。

<a name="remarks"></a>备注
-------

不能与属性数据类型修饰符组合 DEVPROP_TYPE_SECURITY_DESCRIPTOR。

### <a name="setting-a-property-of-this-type"></a>设置此属性类型

若要设置其基本数据类型为 DEVPROP_TYPE_SECURITY_DESCRIPTOR 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_SECURITY_DESCRIPTOR，参数设置*PropertyBuffer*参数指向包含可变长度 SECURITY_DESCRIPTOR 结构的缓冲区的指针和设置*PropertyBufferSize*参数大小 （字节） 的安全描述符结构。

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

 

 





