---
title: ACPI_ENUM_CHILD_NEXT 宏
description: ACPI_ENUM_CHILD_NEXT 宏计算一个指针，该指针指向一个可变长度 ACPI_ENUM_CHILD 结构数组中的下一个 ACPI_ENUM_CHILD 结构。
ms.assetid: 1ff37770-b0ea-4275-9568-611ec125a0b6
keywords:
- ACPI_ENUM_CHILD_NEXT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0082e2a8ec9ca30d6aeed8e8725e15b12bef5b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824113"
---
# <a name="acpi_enum_child_next-macro"></a>ACPI\_枚举\_子\_下一个宏


ACPI\_ENUM\_子\_下一个宏计算一个指针，该指针指向可变长度 ACPI\_枚举\_子结构的数组中的下一个[**acpi\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_NEXT(
    Child
);
```

<a name="parameters"></a>参数
----------

*子*   
一个指针，指向类型为 ACPI 的变量\_枚举\_子元素，该元素将返回一个非对齐指针，该指针指向一个可变长度 ACPI\_枚举\_子结构数组中的下一个 ACPI\_枚举\_子结构。

<a name="return-value"></a>返回值
------------

指向下一个 ACPI\_枚举的指针\_子结构的数组，该数组位于可变长度 ACPI\_枚举\_子结构的数组中。

<a name="remarks"></a>备注
-------

驱动程序使用[**IOCTL\_acpi\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求，以检索[**ACPI\_枚举\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)子集中的子设备名称的数组\_输出\_缓冲区请求，驱动程序可以使用此宏确定指向输出缓冲区包含的**子**数组中的可变长度 ACPI\_枚举\_子结构的一系列指针。

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
<td>桌面</td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Acpiioct （包括 Acpiioct）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)

[**ACPI\_枚举\_子\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)

[**IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)

 

 




