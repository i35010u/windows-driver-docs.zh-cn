---
title: ACPI_METHOD_ARGUMENT_LENGTH 宏
description: ACPI_METHOD_ARGUMENT_LENGTH 宏将计算可变长度 ACPI_METHOD_ARGUMENT 结构的大小（以字节为单位），该结构包含指定大小的数据（以字节为单位）。
ms.assetid: 8329c2eb-a787-4590-8de9-95078bbb85da
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c12ba630f51ae906db73937c91da531c00fddfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824067"
---
# <a name="acpi_method_argument_length-macro"></a>ACPI\_方法\_参数\_长度宏


ACPI\_方法\_参数\_LENGTH 宏以字节为单位计算包含指定大小的数据（以字节为单位）的可变长度[**ACPI\_\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)的大小（以字节为单位）。

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
ACPI\_方法的**数据**数组中数据的大小（以字节为单位）\_参数结构。

<a name="return-value"></a>返回值
------------

可变长度 ACPI\_方法\_参数结构的大小（以字节为单位），该**数据**数组的大小为*DataLength*。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算可变长度 ACPI\_方法的所需大小（以字节为单位），该\_方法可包含指定大小的**数据**数组（以字节为单位）。

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

 

 




