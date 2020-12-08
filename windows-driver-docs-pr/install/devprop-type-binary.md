---
title: DEVPROP_TYPE_BINARY
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_BINARY 标识符表示数据类型为字节类型的无符号值的数组。
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
ms.openlocfilehash: 858c1aa740f041ba88b6e89f9af9468fa101dae1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834525"
---
# <a name="devprop_type_binary"></a>DEVPROP_TYPE_BINARY


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_BINARY 标识符表示数据类型为字节类型的无符号值的数组。

<a name="remarks"></a>备注
-------

DEVPROP_TYPE_BINARY 属性类型不能与属性数据类型修饰符结合。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_BINARY 的属性，请调用相应的 SetupDiSet *Xxx* 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_BINARY，将 *PropertyBuffer* 参数设置为指向包含 BYTE 值数组的缓冲区的指针，并将 *PropertyBufferSize* 参数设置为缓冲区的大小（以字节为单位）。

-   根据需要设置其余函数参数来设置属性。

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

 

 





