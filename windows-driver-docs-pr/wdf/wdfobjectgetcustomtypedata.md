---
title: WdfObjectGetCustomTypeData macro
description: WdfObjectGetCustomTypeData 宏检索驱动程序之前使用 framework 对象和自定义类型相关联的数据。
ms.assetid: 60A6546B-84C6-4A53-BAA1-3719DCBA63B4
keywords:
- WdfObjectGetCustomTypeData macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d51725eb8d1740c10024987ddba5cb15c7f9e9c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385738"
---
# <a name="wdfobjectgetcustomtypedata-macro"></a>WdfObjectGetCustomTypeData macro


\[适用于 KMDF 和 UMDF\]

**WdfObjectGetCustomTypeData**宏检索驱动程序之前使用 framework 对象和自定义类型相关联的数据。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PULONG WdfObjectGetCustomTypeData(
  [in]  Handle,
  [in]  Type
);
```

<a name="parameters"></a>Parameters
----------

*处理*\[中\]  
Framework 对象的句柄。

*类型*\[中\]  
自定义类型的符号名称。

<a name="return-value"></a>返回值
------------

**WdfObjectGetCustomTypeData**返回该驱动程序与 framework 对象和到上一个调用中的自定义类型相关联的数据[ **WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)。

<a name="remarks"></a>备注
-------

有关对象驱动程序类型的详细信息，请参阅[Framework 对象自定义类型](https://msdn.microsoft.com/library/windows/hardware/hh406457)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.11</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 






