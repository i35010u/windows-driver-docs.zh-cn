---
title: WDF_DECLARE_CUSTOM_TYPE 宏
description: WDF_DECLARE_CUSTOM_TYPE 宏为驱动程序的自定义类型创建一个名称和一个访问器方法。
keywords:
- WDF_DECLARE_CUSTOM_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee0075e041232281e87211fb5e52af205e79e73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825287"
---
# <a name="wdf_declare_custom_type-macro"></a>WDF_DECLARE_CUSTOM_TYPE 宏


\[适用于 KMDF 和 UMDF\]

**WDF_DECLARE_CUSTOM_TYPE** 宏为驱动程序的自定义类型创建一个名称和一个访问器方法。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_DECLARE_CUSTOM_TYPE(
    _customtype
);
```

<a name="parameters"></a>参数
----------

*_customtype*   
自定义类型的驱动程序定义的名称。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

调用 **WDF_DECLARE_CUSTOM_TYPE** 时，驱动程序将定义其自己的自定义类型名称。 选择自定义类型名称时，请选择特定于该驱动程序域的名称。 作为约定，不要使用前缀 *Wdf* 来启动自定义类型名称。

有关对象自定义类型的详细信息，请参阅 [框架对象自定义类型](./framework-object-custom-types.md)。

<a name="examples"></a>示例
--------

下面的代码示例调用 **WDF_DECLARE_CUSTOM_TYPE** 宏来声明 MY_CUSTOM_TYPE 自定义类型名称。 驱动程序必须将此行放在声明全局数据的驱动程序区域中，通常是标头文件。

```cpp
WDF_DECLARE_CUSTOM_TYPE(MY_CUSTOM_TYPE)
```

下面的代码示例创建一个请求对象，然后使用 [**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md) 方法将 **MY_CUSTOM_TYPE** 自定义类型与请求对象相关联。

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


[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

