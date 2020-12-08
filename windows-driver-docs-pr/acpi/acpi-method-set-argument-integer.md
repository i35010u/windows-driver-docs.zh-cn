---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏
description: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏为单个整数值设置 ACPI_METHOD_ARGUMENT 结构的成员。
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: be900bf984739c23cb2ba6c649b6755233256f87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789503"
---
# <a name="acpi_method_set_argument_integer-macro"></a>ACPI \_ 方法 \_ 集 \_ 参数 \_ 整数宏


ACPI \_ 方法 \_ 集 \_ 参数 \_ INTEGER 宏为单个整数值设置 [**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的成员。

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
指向 ACPI \_ 方法 \_ 自变量结构的指针。

*IntData*   
类型 ULONG 的整数值。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置 ACPI \_ 方法 \_ 参数结构的成员，该参数结构提供类型为 ULONG 的单个整数值。

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
