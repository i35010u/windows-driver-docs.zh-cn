---
title: DEVPROP_TYPE_ERROR
description: DEVPROP_TYPE_ERROR 标识符表示 WINERROR.H 中定义的 Microsoft Win32 错误代码值的基本数据类型标识符。
ms.assetid: fe8fa3de-a984-4c6f-902f-5eda24402a65
keywords:
- DEVPROP_TYPE_ERROR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_ERROR
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: def32fa4532ec5752f971f991512bf315ab026bd
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715554"
---
# <a name="devprop_type_error"></a>DEVPROP_TYPE_ERROR


DEVPROP_TYPE_ERROR 标识符表示 WINERROR.H 中定义的 Microsoft Win32 错误代码值的基本数据类型标识符。

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md) 还为 NTSTATUS 错误代码值定义了一个 [**DEVPROP_TYPE_NTSTATUS**](devprop-type-ntstatus.md) 的基本数据类型标识符。

只能将 DEVPROP_TYPE_ERROR 与 [**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md) 的属性数据类型修饰符组合在一起。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_ERROR 的属性，请调用相应的 SetupDiSet*Xxx* 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_ERROR。

-   将 *PropertyBuffer* 参数设置为一个指向缓冲区的指针，该缓冲区可包含至少一个 Win32 错误代码值。

-   将 *PropertyBufferSize* 参数设置为 `sizeof(ULONG)` 。

-   根据需要设置其余函数参数来设置属性。

### <a name="retrieving-the-descriptive-text-for-a-win32-error-code-value"></a>检索 Win32 错误代码值的描述性文本

若要检索与 Win32 错误代码关联的描述性文本，请调用 Windows SDK) 中 (记录的 [**FormatMessage**](/windows/win32/api/winbase/nf-winbase-formatmessage) 函数，如下所示：

-   在 *dwflags* 参数的值中包含 FORMAT_MESSAGE_FROM_SYSTEM 标志。

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

## <a name="see-also"></a>请参阅


[**DEVPROP_TYPE_NTSTATUS**](devprop-type-ntstatus.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

