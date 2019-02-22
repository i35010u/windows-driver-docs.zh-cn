---
title: DEVPROP_TYPE_NTSTATUS
description: DEVPROP_TYPE_NTSTATUS 标识符表示在 Ntstatus.h 中定义的 NTSTATUS 状态代码值的基本数据类型标识符。
ms.assetid: 7593d24d-8e89-409e-9047-0c14268b8e62
keywords:
- DEVPROP_TYPE_NTSTATUS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_NTSTATUS
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf8ded26b336b57c798ec9085c97824a77244f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546497"
---
# <a name="devproptypentstatus"></a>DEVPROP_TYPE_NTSTATUS


DEVPROP_TYPE_NTSTATUS 标识符表示在 Ntstatus.h 中定义的 NTSTATUS 状态代码值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](https://msdn.microsoft.com/library/windows/hardware/ff553515)还定义了[ **DEVPROP_TYPE_ERROR** ](devprop-type-error.md) Microsoft 的基本数据类型标识符Win32 错误代码值。

你可以组合只能使用 DEVPROP_TYPE_NTSTATUS [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_NTSTATUS 的属性，调用对应 **SetupDiSet * * * Xxx*属性函数和集函数的输入参数，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_NTSTATUS 参数。

- 设置*PropertyBuffer*参数指向的缓冲区可包含至少一个 NTSTATUS 值。

- 设置*PropertyBufferSize*参数<strong>sizeof (</strong>NTSTATUS<strong>)</strong>。

- 根据需要设置剩余函数参数设置的属性。

### <a name="retrieving-the-descriptive-text-for-a-ntstatus-error-code-value"></a>检索的说明性文本的 NTSTATUS 错误代码值

若要检索与 NTSTATUS 错误代码值相关联的描述性文本，请调用**FormatMessage**函数 （Windows SDK 中所述），如下所示：

-   值中包括 FORMAT_MESSAGE_FROM_SYSTEM 标志和 FORMAT_MESSAGE_FROM_HMODULE 标志的按位 OR *dwflags*参数。

-   设置*lpSource*参数的句柄*NtDLL.dll*模块，这是说明性文本的源。

-   设置*dwMessageID*参数的错误代码值。

-   根据需要设置其他选项和参数来检索的说明性文本。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows Vista 和更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DEVPROP_TYPE_ERROR**](devprop-type-error.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






