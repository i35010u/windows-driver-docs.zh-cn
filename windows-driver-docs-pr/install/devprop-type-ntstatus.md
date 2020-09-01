---
title: DEVPROP_TYPE_NTSTATUS
description: DEVPROP_TYPE_NTSTATUS 标识符表示在 Ntstatus 中定义的 NTSTATUS 状态代码值的基本数据类型标识符。
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
ms.openlocfilehash: 3004ab8097b1f6dfe0e347659b8f99f2e184a1de
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096047"
---
# <a name="devprop_type_ntstatus"></a>DEVPROP_TYPE_NTSTATUS


DEVPROP_TYPE_NTSTATUS 标识符表示在 Ntstatus 中定义的 NTSTATUS 状态代码值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md) 还为 Microsoft Win32 错误代码值定义 [**DEVPROP_TYPE_ERROR**](devprop-type-error.md) 的基本数据类型标识符。

只能将 DEVPROP_TYPE_NTSTATUS 与 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 的属性数据类型修饰符组合在一起。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_NTSTATUS 的属性，请调用相应的 **SetupDiSet**_Xxx_ 属性函数并按如下所示设置函数输入参数：

- 将 *PropertyType* 参数设置为 DEVPROP_TYPE_NTSTATUS。

- 将 *PropertyBuffer* 参数设置为一个指向缓冲区的指针，该缓冲区可包含至少一个 NTSTATUS 值。

- 将 *PropertyBufferSize* 参数设置为 <strong>sizeof (</strong>NTSTATUS<strong>) </strong>。

- 根据需要设置其余函数参数来设置属性。

### <a name="retrieving-the-descriptive-text-for-a-ntstatus-error-code-value"></a>检索 NTSTATUS 错误代码值的描述性文本

若要检索与 NTSTATUS 错误代码值相关联的描述性文本，请调用 **FormatMessage** 函数 (在 Windows SDK 中记录) 如下所示：

-   在 *dwflags* 参数的值中包含 FORMAT_MESSAGE_FROM_SYSTEM 标志和 FORMAT_MESSAGE_FROM_HMODULE 标志的按位 "或"。

-   将 *lpSource* 参数设置为 *NtDLL.dll* 模块的句柄，它是说明性文本的源。

-   将 *dwMessageID* 参数设置为错误代码值。

-   根据需要设置其他选项和参数以检索说明性文本。

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
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DEVPROP_TYPE_ERROR**](devprop-type-error.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

