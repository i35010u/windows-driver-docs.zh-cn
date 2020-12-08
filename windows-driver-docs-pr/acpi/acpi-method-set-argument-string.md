---
title: ACPI_METHOD_SET_ARGUMENT_STRING 宏
description: ACPI_METHOD_SET_ARGUMENT_STRING 宏为字符串值设置 ACPI_METHOD_ARGUMENT 结构的成员。
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bb0706a97ddfb72ba646f5d804d9548ef9612b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789505"
---
# <a name="acpi_method_set_argument_string-macro"></a>ACPI \_ 方法 \_ 集 \_ 参数 \_ 字符串宏


ACPI \_ 方法 \_ 集 \_ 参数 \_ 字符串宏为字符串值设置 [**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的成员。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_STRING(
    Argument,
    StrData
);
```

<a name="parameters"></a>参数
----------

*实际*   
指向 ACPI \_ 方法 \_ 自变量结构的指针。

*StrData*   
指向以 NULL 结尾的 ASCII 字符串的指针。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置 ACPI \_ 方法 \_ 参数结构的成员，该参数结构提供以 NULL 结尾的 ASCII 字符串。

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
<td>台式机</td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Acpiioct (包含 Acpiioct) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ACPI \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)
