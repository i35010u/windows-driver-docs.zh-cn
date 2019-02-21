---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏
description: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏设置单个整数值的 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: a79f9149-0ffe-483f-a45e-427b05ff0a11
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 61fbedf536c27bd6374c8a422e66bb7d28a37c29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534756"
---
# <a name="acpimethodsetargumentinteger-macro"></a>ACPI\_方法\_设置\_自变量\_整数宏


ACPI\_方法\_设置\_自变量\_整数宏设置的成员[ **ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)单个整数值的结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_INTEGER(
    MethodArgument,
    IntData
);
```

<a name="parameters"></a>参数
----------

*MethodArgument*   
指向 ACPI\_方法\_参数结构。

*IntData*   
类型为 ULONG 一个整数值。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置成员的 ACPI\_方法\_参数结构，用于提供类型为 ULONG 单个整数值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Acpiioct.h （包括 Acpiioct.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125) 
