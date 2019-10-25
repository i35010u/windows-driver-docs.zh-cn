---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏计算可变长度 ACPI_ENUM_CHILD 结构的大小（以字节为单位）。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 365671f8c38d1ca707a4dd58b4196d5c72b8f302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824128"
---
# <a name="acpi_enum_child_length_from_child-macro"></a>ACPI\_枚举\_子\_长度\_从\_子宏


\_子宏的 ACPI\_枚举\_子\_长度\_计算可变长度[**ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)结构的大小（以字节为单位）。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>参数
----------

*子*   
一个指针，指向用于计算结构的大小（以字节为单位）的 ACPI\_枚举\_子类型的结构。

<a name="return-value"></a>返回值
------------

ACPI\_枚举 *\_子结构的子*结构的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算[**acpi\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)结构的 ACPI\_枚举\_子结构的大小（以字节为单位），\_输出\_缓冲结构。

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

 

 




