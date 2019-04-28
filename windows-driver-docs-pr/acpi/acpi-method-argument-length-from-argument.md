---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT macro
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏计算大小 （字节） ACPI_METHOD_ARGUMENT 结构的数据数组中包含的数据。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86579c407b4219c0e8ca4ac89d2bdfdb4e2589f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328871"
---
# <a name="acpimethodargumentlengthfromargument-macro"></a>ACPI\_方法\_自变量\_长度\_FROM\_参数宏


ACPI\_方法\_自变量\_长度\_FROM\_参数宏计算大小 （字节） 的数据数组中包含的数据[ **ACPI\_方法\_自变量**](https://msdn.microsoft.com/library/windows/hardware/ff536125)结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>Parameters
----------

*自变量*   
指向 ACPI\_方法\_参数结构。

<a name="return-value"></a>返回值
------------

大小 （字节） 中包含的数据**数据**ACPI 的数组\_方法\_参数结构*参数*指向。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来确定大小 （字节） 中的数据**数据**ACPI 的数组\_方法\_参数结构。

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


[**ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)

 

 




