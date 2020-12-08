---
title: ACPI_ENUM_CHILD_NEXT 宏
description: ACPI_ENUM_CHILD_NEXT 宏将计算指向 ACPI_ENUM_CHILD 结构的可变长度数组中的下一个 ACPI_ENUM_CHILD 结构的指针。
keywords:
- ACPI_ENUM_CHILD_NEXT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbac74f72e7a563f772f8ac29890b19ef9725485
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789530"
---
# <a name="acpi_enum_child_next-macro"></a>ACPI \_ 枚举 \_ 子 \_ 下一个宏


ACPI \_ 枚举 \_ 子 \_ 下一个宏计算指向可变长度 acpi 枚举子结构数组中的下一个 [**ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child) 结构的指针 \_ \_ 。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_NEXT(
    Child
);
```

<a name="parameters"></a>参数
----------

*子代*   
指向 ACPI 枚举子级类型的变量的指针， \_ \_ \_ \_ 在可变长度 acpi \_ 枚举子结构的数组中，该指针将向下一个 ACPI 枚举子结构返回非对齐指针 \_ 。

<a name="return-value"></a>返回值
------------

指向下一个 ACPI \_ 枚举 \_ 子结构的指针，该元素位于可变长度 acpi \_ 枚举子结构的数组中 \_ 。

<a name="remarks"></a>备注
-------

驱动程序使用 [**IOCTL \_ acpi \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children) 请求在 [**ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer) 请求中检索子设备名称的数组之后，驱动程序可以使用此宏确定指向 \_ \_ 输出缓冲区包含的 **子** 数组中的可变长度 ACPI 枚举子结构的指针序列。

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


[**ACPI \_ 枚举 \_ 子级**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)

[**ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)

[**IOCTL \_ ACPI \_ 枚举 \_ 子级**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)

 

