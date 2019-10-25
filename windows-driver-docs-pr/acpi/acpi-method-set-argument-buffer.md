---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏
description: ACPI_METHOD_SET_ARGUMENT_BUFFER 宏为数据缓冲区中提供的自定义数据设置 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords:
- ACPI_METHOD_SET_ARGUMENT_BUFFER 宏 ACPI 设备
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c29600dc80179b5f8acd81536ff21457ea42103b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824061"
---
# <a name="acpi_method_set_argument_buffer-macro"></a>ACPI\_方法\_设置\_参数\_BUFFER 宏


ACPI\_方法\_SET\_参数\_BUFFER 宏为数据缓冲区中提供的自定义数据设置[**ACPI\_方法的成员\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_BUFFER(
    Argument,
    BuffData,
    BuffLength
);
```

<a name="parameters"></a>参数
----------

*参数*   
指向 ACPI\_方法\_参数结构的指针。

*BuffData*   
指向包含自定义数据的数据缓冲区的指针。

*BuffLength*   
自定义数据的大小（以字节为单位）。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏设置提供自定义数据的 ACPI\_方法\_参数结构的成员。

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
