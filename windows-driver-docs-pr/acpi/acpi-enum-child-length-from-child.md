---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD macro
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏计算的大小，以字节为单位的长度可变的 ACPI_ENUM_CHILD 结构。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c750fe8d6cbcce2c3e8d0b2cb347c143faefc38b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355900"
---
# <a name="acpienumchildlengthfromchild-macro"></a>ACPI\_ENUM\_子\_长度\_FROM\_子宏


ACPI\_ENUM\_子\_长度\_FROM\_子宏计算大小 （字节） 长度可变[ **ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>Parameters
----------

*子*   
指向一个结构类型 ACPI\_枚举\_子要为其计算大小 （字节） 结构。

<a name="return-value"></a>返回值
------------

大小 （字节） ACPI\_ENUM\_子结构*子*指向。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算的大小，以字节为单位的 ACPI\_ENUM\_中的子结构[ **ACPI\_枚举\_子级\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)结构。

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

 

 




