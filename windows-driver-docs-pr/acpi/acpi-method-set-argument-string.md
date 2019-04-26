---
title: ACPI_METHOD_SET_ARGUMENT_STRING 宏
description: ACPI_METHOD_SET_ARGUMENT_STRING 宏设置一个字符串值的 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: e0c037a9-65b6-4d6a-9ed6-d9296c14df07
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7278e3c3bebed21c4330839a01a728be90f3773b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328845"
---
# <a name="acpimethodsetargumentstring-macro"></a>ACPI\_方法\_设置\_自变量\_字符串宏


ACPI\_方法\_设置\_自变量\_字符串宏设置的成员[ **ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)一个字符串值的结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_STRING(
    Argument,
    StrData
);
```

<a name="parameters"></a>Parameters
----------

*自变量*   
指向 ACPI\_方法\_参数结构。

*StrData*   
指向以 NULL 结尾的 ASCII 字符串的指针。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置成员的 ACPI\_方法\_参数结构，它提供了一个以 NULL 结尾的 ASCII 字符串。

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
<td><p>Header</p></td>
<td>Acpiioct.h （包括 Acpiioct.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125) 
