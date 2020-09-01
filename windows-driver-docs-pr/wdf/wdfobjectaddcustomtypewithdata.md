---
title: WdfObjectAddCustomTypeWithData 宏
description: WdfObjectAddCustomTypeWithData 宏将框架对象与自定义类型相关联，并选择性地将此对与数据缓冲区和事件回调函数相关联。
ms.assetid: 237F9BAA-A2E2-4F20-B52E-8F093B326E45
keywords:
- WdfObjectAddCustomTypeWithData 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41243825aae447d0da19f623fd3cee20f6bb15a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187319"
---
# <a name="wdfobjectaddcustomtypewithdata-macro"></a>WdfObjectAddCustomTypeWithData 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectAddCustomTypeWithData**宏将框架对象与自定义类型相关联，并选择性地将此对与数据缓冲区和事件回调函数相关联。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomTypeWithData(
    _handle,
    _type,
    _data,
    _cleanup,
    _destroy
);
```

<a name="parameters"></a>参数
----------

*_handle*   
框架对象的句柄。

*_type*   
自定义类型的驱动程序定义名称。

*_data*   
指向驱动程序提供的数据缓冲区的指针，或为 NULL。 此参数是可选的。

*_cleanup*   
指向驱动程序的 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 回调函数的指针，或为 NULL。 此参数是可选的。

*_destroy*   
指向驱动程序的 [*EvtDestroyCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy) 回调函数的指针，或为 NULL。 此参数是可选的。

<a name="return-value"></a>返回值
------------

如果操作成功，则**WdfObjectAddCustomTypeWithData**返回 STATUS_SUCCESS。 否则，此方法可能会返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>STATUS_OBJECT_PATH_INVALID</strong></td>
<td><p>指定的句柄不能添加自定义类型。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td><p>未能分配自定义类型。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_OBJECT_NAME_EXISTS</strong></td>
<td><p>驱动程序已添加指定的自定义类型。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_DELETE_PENDING</strong></td>
<td><p>正在删除 Handle 参数指定的对象。 在这种情况下，框架不添加自定义类型。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

如果你的驱动程序使用指向数据缓冲区的指针调用 **WdfObjectAddCustomTypeWithData** ，则驱动程序可以提供 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 或 [*EvtDestroyCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy) 回调函数，以便在删除对象时解除分配内存缓冲区。

有关对象自定义类型的详细信息，请参阅 [框架对象自定义类型](./framework-object-custom-types.md)。

有关代码示例，请参阅 [**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)。

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
<td><p>Header</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

