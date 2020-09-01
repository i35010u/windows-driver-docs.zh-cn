---
title: ACPI_METHOD_SET_ARGUMENT_STRING 宏
description: ACPI_METHOD_SET_ARGUMENT_STRING 宏为字符串值设置 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: e0c037a9-65b6-4d6a-9ed6-d9296c14df07
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e31a6a64ee5c9d3d504232bb5acb9347e897080d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184857"
---
# <a name="acpi_method_set_argument_string-macro"></a>ACPI \_ 方法 \_ 集 \_ 参数 \_ 字符串宏


ACPI \_ 方法 \_ 集 \_ 参数 \_ 字符串宏为字符串值设置 [**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的成员。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_STRING(
    Argument,
    StrData
);
```

<a name="parameters"></a>参数
----------

*实际*   
指向 ACPI \_ 方法 \_ 自变量结构的指针。

*StrData*   
指向以 NULL 结尾的 ASCII 字符串的指针。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置 ACPI \_ 方法 \_ 参数结构的成员，该参数结构提供以 NULL 结尾的 ASCII 字符串。

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