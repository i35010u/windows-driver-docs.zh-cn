---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD macro
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏计算的大小，以字节为单位的长度可变的 ACPI_ENUM_CHILD 结构。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb682142fe13b46dc324d52379360ac4422c29e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533248"
---
# <a name="acpienumchildlengthfromchild-macro"></a>ACPI\_ENUM\_子\_长度\_FROM\_子宏


ACPI\_ENUM\_子\_长度\_FROM\_子宏计算大小 （字节） 长度可变[ **ACPI\_枚举\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)结构。

<a name="syntax"></a>语法
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>参数
----------

*子*   
指向一个结构类型 ACPI\_枚举\_子要为其计算大小 （字节） 结构。

<a name="return-value"></a>返回值
------------

大小 （字节） ACPI\_ENUM\_子结构*子*指向。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏来计算的大小，以字节为单位的 ACPI\_ENUM\_中的子结构[ **ACPI\_枚举\_子级\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536112)结构。

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
<td>Acpiioct.h （包括 Acpiioct.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI\_ENUM\_CHILD**](https://msdn.microsoft.com/library/windows/hardware/ff536109)

[**ACPI\_ENUM\_CHILDREN\_OUTPUT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff536112)

 

 




