---
title: ACPI_METHOD_NEXT_ARGUMENT 宏
description: ACPI_METHOD_NEXT_ARGUMENT 结构返回指向 ACPI_METHOD_ARGUMENT 结构数组中的下一个 ACPI_METHOD_ARGUMENT 结构的指针。
ms.assetid: c723b11b-1657-4a78-a6a1-26bd916604a4
keywords:
- ACPI_METHOD_NEXT_ARGUMENT 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a78bcd3377346f1a75e221699f577da6920f43d3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184501"
---
# <a name="acpi_method_next_argument-macro"></a>ACPI \_ 方法 \_ 下一个 \_ 参数宏


ACPI \_ 方法 \_ NEXT \_ 参数结构返回一个指针，指向 acpi 方法参数结构数组中的下一个 [**acpi \_ 方法 \_ 自变量**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构 \_ \_ 。

<a name="syntax"></a>语法
------

```cpp
 ACPI_METHOD_NEXT_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>参数
----------

*实际*   
一个指针，指向 ACPI 方法参数结构 \_ \_ 数组中的 acpi 方法参数结构 \_ \_ 。

<a name="return-value"></a>返回值
------------

一个指针，指向 \_ \_ acpi \_ 方法参数结构数组中的下一个 acpi 方法参数结构 \_ 。

<a name="remarks"></a>备注
-------

给定一个指向 \_ \_ 此类结构数组中的 ACPI 方法自变量结构的指针，驱动程序可以使用此宏来计算指向数组中下一个结构的指针（如果存在）。

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