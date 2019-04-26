---
title: ACPI_METHOD_NEXT_ARGUMENT 宏
description: ACPI_METHOD_NEXT_ARGUMENT 结构返回一个指向 ACPI_METHOD_ARGUMENT 结构数组中的下一步 ACPI_METHOD_ARGUMENT 结构。
ms.assetid: c723b11b-1657-4a78-a6a1-26bd916604a4
keywords:
- ACPI_METHOD_NEXT_ARGUMENT 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed7d06635ff22f61562ff5cc406d7030cbeb9f0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328841"
---
# <a name="acpimethodnextargument-macro"></a>ACPI\_方法\_下一步\_参数宏


ACPI\_方法\_下一步\_参数结构返回一个指向下一步[ **ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)结构数组的 ACPI\_方法\_参数结构。

<a name="syntax"></a>语法
------

```cpp
 ACPI_METHOD_NEXT_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>Parameters
----------

*自变量*   
指向 ACPI\_方法\_参数结构数组中的 ACPI\_方法\_参数结构。

<a name="return-value"></a>返回值
------------

指向下一步 ACPI\_方法\_参数结构数组中的 ACPI\_方法\_参数结构。

<a name="remarks"></a>备注
-------

提供一个指向 ACPI\_方法\_参数结构中此类结构的数组，驱动程序可以使用此宏来计算指向数组中的下一步结构如果存在。

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
