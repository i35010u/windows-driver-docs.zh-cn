---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏将计算可变长度 ACPI_ENUM_CHILD 结构的大小（以字节为单位）。
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eeafe4ab2d43ebf60e81acff32c46babe5ed566
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787998"
---
# <a name="acpi_enum_child_length_from_child-macro"></a>\_ \_ \_ \_ 子宏中的 ACPI 枚举子长度 \_


\_子宏中的 ACPI 枚举 \_ 子 \_ LENGTH \_ \_ 计算可变长度 [**ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)结构的大小（以字节为单位）。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>参数
----------

*子代*   
指向为 \_ \_ 其计算结构的大小（以字节为单位）的 ACPI 枚举子级类型的结构的指针。

<a name="return-value"></a>返回值
------------

\_ \_ *子元素* 指向的 ACPI 枚举子结构的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算 \_ \_ [**acpi \_ 枚举 \_ \_ \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer) 结构中 acpi 枚举子结构的大小（以字节为单位）。

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

 

