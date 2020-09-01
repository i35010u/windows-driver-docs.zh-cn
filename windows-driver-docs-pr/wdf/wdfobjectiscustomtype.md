---
title: WdfObjectIsCustomType 宏
description: WdfObjectIsCustomType 宏确定框架对象是否为指定的自定义类型。
ms.assetid: EE3CC41D-6FBA-49A2-A2A0-C7E818F6FAAA
keywords:
- WdfObjectIsCustomType 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cebeadd6579bb59c39575c8dff8e09ef2397cdbe
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188685"
---
# <a name="wdfobjectiscustomtype-macro"></a>WdfObjectIsCustomType 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectIsCustomType**宏确定框架对象是否为指定的自定义类型。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOLEAN WdfObjectIsCustomType(
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

如果指定的对象属于指定的自定义类型，则返回 TRUE。 否则，返回 FALSE。

<a name="remarks"></a>备注
-------

有关对象自定义类型的详细信息，请参阅 [框架对象自定义类型](./framework-object-custom-types.md)。

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

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

 

