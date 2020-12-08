---
title: DEVPROP_TYPE_SECURITY_DESCRIPTOR
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_SECURITY_DESCRIPTOR 标识符表示表示数据类型为可变长度、自相关、SECURITY_DESCRIPTOR 类型化安全描述符的基本数据类型标识符。
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
ms.openlocfilehash: c66aa64271a7a408f717e591d4462a93e9fd12e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815325"
---
# <a name="devprop_type_security_descriptor"></a>DEVPROP_TYPE_SECURITY_DESCRIPTOR


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_SECURITY_DESCRIPTOR 标识符表示表示数据类型为可变长度、自相关、SECURITY_DESCRIPTOR 类型化安全描述符的基本数据类型标识符。

<a name="remarks"></a>备注
-------

不能将 DEVPROP_TYPE_SECURITY_DESCRIPTOR 与属性数据类型修饰符结合。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_SECURITY_DESCRIPTOR 的属性，请调用相应的 **SetupDiSet * Xxx*** 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_SECURITY_DESCRIPTOR，将 *PropertyBuffer* 参数设置为指向缓冲区的指针，该缓冲区包含可变长度 SECURITY_DESCRIPTOR 结构，并将 *PropertyBufferSize* 参数设置为安全描述符结构的大小（以字节为单位）。

-   根据需要设置其他函数输入参数来设置属性。

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
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

 

 





