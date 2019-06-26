---
title: ACPI_METHOD_ARGUMENT_LENGTH 宏
description: ACPI_METHOD_ARGUMENT_LENGTH 宏计算大小 （字节），包含指定的大小，以字节为单位的数据的可变长度 ACPI_METHOD_ARGUMENT 结构。
ms.assetid: 8329c2eb-a787-4590-8de9-95078bbb85da
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8628b88e6acdbb6f4a9ddad4f1957a832c6dca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355882"
---
# <a name="acpimethodargumentlength-macro"></a>ACPI\_方法\_自变量\_长度宏


ACPI\_方法\_自变量\_长度宏计算大小 （字节） 长度可变[ **ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构，其中包含指定的大小，以字节为单位的数据。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH(
    DataLength
);
```

<a name="parameters"></a>Parameters
----------

*DataLength*   
大小 （字节） 中的数据**数据**ACPI 的数组\_方法\_参数结构。

<a name="return-value"></a>返回值
------------

大小 （字节） 长度可变的 ACPI\_方法\_可以包含的参数结构**数据**数组，其大小，以字节为单位，都*DataLength*。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算所需的大小，以字节为单位的长度可变的 ACPI\_方法\_可包含的参数结构**数据**数组的指定大小 （字节）。

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


[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)

 

 




