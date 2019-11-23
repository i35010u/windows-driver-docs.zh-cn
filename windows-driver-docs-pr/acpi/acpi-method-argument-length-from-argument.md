---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏计算 ACPI_METHOD_ARGUMENT 结构的数据数组中包含的数据的大小（以字节为单位）。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bcd86f5d9679552f2f8c7db47ac69292227201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824069"
---
# <a name="acpi_method_argument_length_from_argument-macro"></a>ACPI\_方法\_参数\_长度\_从\_参数宏


ACPI\_方法\_参数\_长度\_从\_参数中宏计算[**ACPI\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)的数据数组中包含的数据的大小（以字节为单位）\_参数结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>参数
----------

*参数*   
指向 ACPI\_方法\_参数结构的指针。

<a name="return-value"></a>返回值
------------

在 ACPI\_方法的**数据**数组中包含的数据的大小（以字节为单位），该*参数*指向的\_参数结构。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来确定 ACPI\_方法的**数据**数组中数据的大小（以字节为单位）\_参数结构。

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
<td><p>标头</p></td>
<td>Acpiioct （包括 Acpiioct）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)

 

 




