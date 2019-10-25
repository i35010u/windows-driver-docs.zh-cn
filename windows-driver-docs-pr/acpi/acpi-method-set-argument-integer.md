---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏
description: ACPI_METHOD_SET_ARGUMENT_INTEGER 宏为单个整数值设置 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: a79f9149-0ffe-483f-a45e-427b05ff0a11
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7107b1678c4f5da1e27fc8af69ed95b06b22ef76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824059"
---
# <a name="acpi_method_set_argument_integer-macro"></a>ACPI\_方法\_设置\_参数\_整数宏


ACPI\_方法\_SET\_参数\_INTEGER 宏为单个整数值设置[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构的成员。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_INTEGER(
    MethodArgument,
    IntData
);
```

<a name="parameters"></a>参数
----------

*MethodArgument*   
指向 ACPI\_方法\_参数结构的指针。

*IntData*   
类型 ULONG 的整数值。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置 ACPI\_方法\_参数结构的成员，该参数结构提供类型为 ULONG 的单个整数值。

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


[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 
