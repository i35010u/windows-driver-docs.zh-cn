---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏
description: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏为数据缓冲区中提供的自定义数据设置 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords:
- ACPI_METHOD_SET_ARGUMENT_BUFFER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9daa7774936c5f06099ac5b376684b51288c84c8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184867"
---
# <a name="acpi_method_set_argument_buffer-macro"></a>ACPI \_ 方法 \_ 集 \_ 参数 \_ 缓冲区宏


ACPI \_ 方法 \_ 集 \_ 参数 \_ 缓冲区宏为数据缓冲区中提供的自定义数据设置 [**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的成员。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_BUFFER(
    Argument,
    BuffData,
    BuffLength
);
```

<a name="parameters"></a>参数
----------

*实际*   
指向 ACPI \_ 方法 \_ 自变量结构的指针。

*BuffData*   
指向包含自定义数据的数据缓冲区的指针。

*BuffLength*   
自定义数据的大小（以字节为单位）。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置 \_ \_ 提供自定义数据的 ACPI 方法参数结构的成员。

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