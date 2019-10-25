---
title: ACPI_METHOD_NEXT_ARGUMENT 宏
description: ACPI_METHOD_NEXT_ARGUMENT 结构返回指向 ACPI_METHOD_ARGUMENT 结构数组中的下一个 ACPI_METHOD_ARGUMENT 结构的指针。
ms.assetid: c723b11b-1657-4a78-a6a1-26bd916604a4
keywords:
- ACPI_METHOD_NEXT_ARGUMENT 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 47c41af603a78680f38c1da856d3e4e7a5c2fb6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824063"
---
# <a name="acpi_method_next_argument-macro"></a>ACPI\_方法\_下一个\_参数宏


ACPI\_方法\_下一个\_参数结构在 ACPI\_方法\_参数结构的数组中返回指向下一个[**acpi\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)的指针。

<a name="syntax"></a>语法
------

```cpp
 ACPI_METHOD_NEXT_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>参数
----------

*参数*   
指向 ACPI\_方法的指针\_ACPI\_方法的数组中的参数结构\_参数结构。

<a name="return-value"></a>返回值
------------

指向下一个 ACPI\_方法的指针\_ACPI\_方法的数组中的参数结构\_参数结构。

<a name="remarks"></a>备注
-------

给定一个指向 ACPI\_方法的指针\_此类结构数组中的参数结构，驱动程序可以使用此宏来计算指向数组中下一个结构的指针（如果存在）。

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
