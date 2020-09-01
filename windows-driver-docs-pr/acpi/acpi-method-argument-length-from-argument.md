---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏计算 ACPI_METHOD_ARGUMENT 结构的数据数组中包含的数据的大小（以字节为单位）。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9698816229affd264fbc0c1b105f95525e8bb1a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184509"
---
# <a name="acpi_method_argument_length_from_argument-macro"></a>\_ \_ \_ \_ 自 \_ 变量宏的 ACPI 方法参数长度


\_ \_ 自变量宏的 ACPI METHOD 参数 \_ LENGTH \_ \_ 计算[**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构的数据数组中包含的数据的大小（以字节为单位）。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>参数
----------

*实际*   
指向 ACPI \_ 方法 \_ 自变量结构的指针。

<a name="return-value"></a>返回值
------------

参数指向的 ACPI **Data** \_ 方法 \_ 参数*Argument*结构的数据数组中包含的数据的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来确定 ACPI **Data** \_ 方法参数结构的数据数组中数据的大小（以字节为单位） \_ 。

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

 

