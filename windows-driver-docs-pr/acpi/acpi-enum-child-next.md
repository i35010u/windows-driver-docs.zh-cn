---
title: ACPI_ENUM_CHILD_NEXT macro
description: ACPI_ENUM_CHILD_NEXT 宏计算到可变长度 ACPI_ENUM_CHILD 结构数组中的下一步 ACPI_ENUM_CHILD 结构的指针。
ms.assetid: 1ff37770-b0ea-4275-9568-611ec125a0b6
keywords:
- ACPI_ENUM_CHILD_NEXT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49af38a832a22bcb06c11e1f5b5986c06506a5ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355890"
---
# <a name="acpienumchildnext-macro"></a>ACPI\_ENUM\_子\_下一步宏


ACPI\_ENUM\_子\_下一步宏计算到下一个指针[ **ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)数组中的结构可变长度 ACPI\_枚举\_子结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_NEXT(
    Child
);
```

<a name="parameters"></a>Parameters
----------

*子*   
指向类型 ACPI 的变量的指针\_ENUM\_要为其返回到下一步 ACPI 的非对齐的指针的子\_枚举\_子结构数组中的长度可变的 ACPI\_枚举\_子结构。

<a name="return-value"></a>返回值
------------

指向下一步 ACPI\_ENUM\_子结构数组中的长度可变的 ACPI\_枚举\_子结构。

<a name="remarks"></a>备注
-------

驱动程序将使用后[ **IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求来检索数组中的子设备名称[ **ACPI\_ENUM\_子级\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)请求，该驱动程序可以使用此宏来确定一系列长度可变的 ACPI指向的指针\_枚举\_中的子结构**子级**输出缓冲区中包含的数组。

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


[**ACPI\_ENUM\_CHILD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)

[**ACPI\_ENUM\_CHILDREN\_OUTPUT\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)

[**IOCTL\_ACPI\_ENUM\_CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)

 

 




