---
title: ACPI_METHOD_ARGUMENT_LENGTH 宏
description: ACPI_METHOD_ARGUMENT_LENGTH 宏将计算可变长度 ACPI_METHOD_ARGUMENT 结构的大小（以字节为单位），该结构包含指定大小的数据（以字节为单位）。
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dadfea48d3bf3ff24c5aa469b8de92741a723b79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789519"
---
# <a name="acpi_method_argument_length-macro"></a>ACPI \_ 方法 \_ 自变量 \_ 长度宏


ACPI \_ 方法 \_ 自 \_ 变量 length 宏计算包含指定大小的数据（以字节为单位）的可变长度 [**ACPI \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的大小（以字节为单位）。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH(
    DataLength
);
```

<a name="parameters"></a>参数
----------

*DataLength*   
ACPI **Data** \_ 方法参数结构的数据数组中数据的大小（以字节为单位） \_ 。

<a name="return-value"></a>返回值
------------

可变长度 ACPI 方法参数结构的大小（以字节为单位）， \_ \_ 该方法可包含大小为 *DataLength* 的 **数据** 数组。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算可变长度 ACPI 方法参数结构的所需大小（以字节为单位）， \_ \_ 该方法可以包含指定大小的 **数据** 数组（以字节为单位）。

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

 

