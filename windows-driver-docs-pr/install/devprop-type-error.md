---
title: DEVPROP_TYPE_ERROR
description: DEVPROP_TYPE_ERROR 标识符表示 WINERROR 中定义的 Microsoft Win32 错误代码值的基本数据类型标识符。H.
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
ms.openlocfilehash: 2e2b32bedfabfca7168f0b24f4c5b1ae9b08d903
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358838"
---
# <a name="devproptypeerror"></a>DEVPROP_TYPE_ERROR


DEVPROP_TYPE_ERROR 标识符表示 WINERROR 中定义的 Microsoft Win32 错误代码值的基本数据类型标识符。H.

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](https://msdn.microsoft.com/library/windows/hardware/ff553515)还定义了[ **DEVPROP_TYPE_NTSTATUS** ](devprop-type-ntstatus.md) NTSTATUS 的基本数据类型标识符错误代码值。

你可以组合只能使用 DEVPROP_TYPE_ERROR [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_ERROR 的属性，调用相应 SetupDiSet*Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_ERROR 参数。

-   设置*PropertyBuffer*参数指向的缓冲区可包含至少一个 Win32 错误代码值。

-   设置*PropertyBufferSize*参数`sizeof(ULONG)`。

-   根据需要设置剩余函数参数设置的属性。

### <a name="retrieving-the-descriptive-text-for-a-win32-error-code-value"></a>为 Win32 错误代码值检索的说明性文本

若要检索与 Win32 错误代码关联的描述性文本，请调用[ **FormatMessage** ](https://msdn.microsoft.com/library/windows/desktop/ms679351)函数 （Windows SDK 中所述），如下所示：

-   值中包括 FORMAT_MESSAGE_FROM_SYSTEM 标志*dwflags*参数。

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
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows Vista 和更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROP_TYPE_NTSTATUS**](devprop-type-ntstatus.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






