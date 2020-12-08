---
title: WdfObjectGetCustomTypeData 宏
description: WdfObjectGetCustomTypeData 宏检索驱动程序以前与框架对象和自定义类型相关联的数据。
keywords:
- WdfObjectGetCustomTypeData 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e00f1b505ea62b0183c283319099272c095908b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790115"
---
# <a name="wdfobjectgetcustomtypedata-macro"></a>WdfObjectGetCustomTypeData 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectGetCustomTypeData** 宏检索驱动程序以前与框架对象和自定义类型相关联的数据。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PULONG WdfObjectGetCustomTypeData(
  [in]  Handle,
  [in]  Type
);
```

<a name="parameters"></a>参数
----------

*句柄* \[中\]  
框架对象的句柄。

*类型* \[中\]  
自定义类型的符号名称。

<a name="return-value"></a>返回值
------------

**WdfObjectGetCustomTypeData** 返回在先前对 [**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)的调用中，驱动程序与框架对象和自定义类型相关联的数据。

<a name="remarks"></a>备注
-------

有关对象驱动程序类型的详细信息，请参阅 [框架对象自定义类型](./framework-object-custom-types.md)。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.11</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

