---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏
description: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏设置数据缓冲区中提供的自定义数据 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords:
- ACPI_METHOD_SET_ARGUMENT_BUFFER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e7d3f5ca7ad3b58d471af4beb33cbf1eb33e6eb2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355878"
---
# <a name="acpimethodsetargumentbuffer-macro"></a>ACPI\_方法\_设置\_自变量\_缓冲区宏


ACPI\_方法\_设置\_自变量\_缓冲区宏设置的成员[ **ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)的数据缓冲区中提供的自定义数据结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_BUFFER(
    Argument,
    BuffData,
    BuffLength
);
```

<a name="parameters"></a>Parameters
----------

*自变量*   
指向 ACPI\_方法\_参数结构。

*BuffData*   
指向包含自定义数据的数据缓冲区的指针。

*BuffLength*   
以字节为单位的自定义数据的大小。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置成员的 ACPI\_方法\_参数提供自定义数据的结构。

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
