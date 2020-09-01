---
title: WdfObjectGetCustomTypeData 宏
description: WdfObjectGetCustomTypeData 宏检索驱动程序以前与框架对象和自定义类型相关联的数据。
ms.assetid: 60A6546B-84C6-4A53-BAA1-3719DCBA63B4
keywords:
- WdfObjectGetCustomTypeData 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e54a69f3bffa5b0c0c20af5999fd4b4f633ad3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188687"
---
# <a name="wdfobjectgetcustomtypedata-macro"></a>WdfObjectGetCustomTypeData 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectGetCustomTypeData**宏检索驱动程序以前与框架对象和自定义类型相关联的数据。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PULONG WdfObjectGetCustomTypeData(
  [in]  Handle,
  [in]  Type
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

## <a name="see-also"></a>另请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

