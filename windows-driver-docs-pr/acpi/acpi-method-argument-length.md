---
title: ACPI_METHOD_ARGUMENT_LENGTH 宏
description: ACPI_METHOD_ARGUMENT_LENGTH 宏将计算可变长度 ACPI_METHOD_ARGUMENT 结构的大小（以字节为单位），该结构包含指定大小的数据（以字节为单位）。
ms.assetid: 8329c2eb-a787-4590-8de9-95078bbb85da
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a9ca5aedad567d53997edc5e82c88bafa6fb20
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184861"
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

可变长度 ACPI 方法参数结构的大小（以字节为单位）， \_ \_ 该方法可包含大小为*DataLength*的**数据**数组。

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
<td>“桌面”</td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Acpiioct (包含 Acpiioct) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)

 

