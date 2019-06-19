---
title: WDF_DECLARE_CUSTOM_TYPE 宏
description: WDF_DECLARE_CUSTOM_TYPE 宏创建的名称和驱动程序的自定义类型的访问器方法。
ms.assetid: DF496E17-B3D4-4983-8506-40810ECAEA3E
keywords:
- WDF_DECLARE_CUSTOM_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7991faa73ee65b01b01ba19c219124f02d6c0d0b
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161568"
---
# <a name="wdfdeclarecustomtype-macro"></a>WDF_DECLARE_CUSTOM_TYPE 宏


\[适用于 KMDF 和 UMDF\]

**WDF_DECLARE_CUSTOM_TYPE**宏创建的名称和驱动程序的自定义类型的访问器方法。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_DECLARE_CUSTOM_TYPE(
    _customtype
);
```

<a name="parameters"></a>Parameters
----------

*_customtype*   
驱动程序定义自定义类型的名称。

<a name="return-value"></a>返回值
------------

此宏不会返回一个值。

<a name="remarks"></a>备注
-------

调用时**WDF_DECLARE_CUSTOM_TYPE**，驱动程序定义自己的自定义类型名称。 当选择自定义的类型名称，选择特定于驱动程序的域的名称。 作为约定，不是从开始你的自定义类型名称前缀*Wdf*。

有关对象的自定义类型的详细信息，请参阅[Framework 对象的自定义类型](https://msdn.microsoft.com/library/windows/hardware/hh406457)。

<a name="examples"></a>示例
--------

下面的代码示例调用**WDF_DECLARE_CUSTOM_TYPE**宏声明 MY_CUSTOM_TYPE 自定义的类型名称。 该驱动程序必须将此行放入声明全局数据，通常标头文件的驱动程序的区域中。

```cpp
WDF_DECLARE_CUSTOM_TYPE(MY_CUSTOM_TYPE)
```

下面的代码示例创建一个请求对象，并使用它[ **WdfObjectAddCustomType** ](wdfobjectaddcustomtype.md)方法将关联起来**MY_CUSTOM_TYPE**具有自定义类型请求对象。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;

WDF_OBJECT_ATTRIBUTES_INIT(&MyRequestObjectAttributes);

status = WdfRequestCreate(
                          &MyRequestObjectAttributes
                          NULL,
                          &Request
                          );

if (!NT_SUCCESS(status)) {
    return status;
}

status = WdfObjectAddCustomType(
                          Request,
                          MY_CUSTOM_TYPE
                          );

if (!NT_SUCCESS(status)) {
    return status;
}
```

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


[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 






