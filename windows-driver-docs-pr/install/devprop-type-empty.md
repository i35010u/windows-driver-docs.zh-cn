---
title: DEVPROP_TYPE_EMPTY
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_EMPTY 标识符表示一个特殊的基本数据类型标识符，该标识符指示属性不存在。
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
ms.openlocfilehash: abe4ae0b25ee5e0cafc7bc7ff0497af214976182
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732545"
---
# <a name="devprop_type_empty"></a>DEVPROP_TYPE_EMPTY


在 Windows Vista 和更高版本的 Windows 中，DEVPROP_TYPE_EMPTY 标识符表示一个特殊的基本数据类型标识符，该标识符指示属性不存在。

<a name="remarks"></a>备注
-------

将此基本数据类型标识符与设备属性函数结合使用，以删除属性。

如果设备属性函数返回此基本数据类型标识符，则该属性不存在。

**DEVPROP_TYPE_EMPTY** 不能与属性数据类型修饰符组合 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 或 [**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md)。

### <a name="deleting-a-property"></a>删除属性

若要删除属性，请调用相应的 SetupDiSet*Xxx* 属性函数并设置函数参数，如下所示：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_EMPTY，将 *PropertyBuffer* 参数设置为 **NULL**，将 *PropertyBufferSize* 参数设置为零。

-   根据需要设置其他函数输入参数来设置属性。

如果在尝试删除不存在的属性时使用 DEVPROP_TYPE_EMPTY，则删除操作将失败，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回 ERROR_NOT_FOUND。

### <a name="retrieving-a-property-that-does-not-exist"></a>正在检索不存在的属性

调用 SetupDiGet*Xxx* 属性函数（该函数尝试检索不存在的设备属性）将失败，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回 ERROR_NOT_FOUND。 调用的 Setupapi.log 属性函数会将 \* *PropertyType*参数设置为 DEVPROP_TYPE_EMPTY。

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

 

