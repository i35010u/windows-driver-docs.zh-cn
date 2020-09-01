---
title: WdfObjectAddCustomType 宏
description: WdfObjectAddCustomType 宏将框架对象与自定义类型关联。
ms.assetid: 750CF669-A436-4571-B474-D5447E0AA64F
keywords:
- WdfObjectAddCustomType 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65bb413376a538f5f9e0b5694cbea8bae90f90e4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189699"
---
# <a name="wdfobjectaddcustomtype-macro"></a>WdfObjectAddCustomType 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectAddCustomType**宏将框架对象与自定义类型关联。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomType(
    _handle,
    _type
);
```

<a name="parameters"></a>参数
----------

*_handle*   
框架对象的句柄。

*_type*   
自定义类型的驱动程序定义名称。

<a name="return-value"></a>返回值
------------

如果操作成功，则**WdfObjectAddCustomType**返回 STATUS_SUCCESS。 否则，此方法可能会返回以下值之一：

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

**WdfObjectAddCustomType** 是 [**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)的简化版本。

有关对象驱动程序类型的详细信息，请参阅 [框架对象自定义类型](./framework-object-custom-types.md)。

<a name="examples"></a>示例
--------

此代码示例演示如何将自定义类型添加到队列。

```cpp
NTSTATUS                status;
WDF_IO_QUEUE_CONFIG     queueConfig;
WDFQUEUE                queue;  

WDF_IO_QUEUE_CONFIG_INIT(&queueConfig,   
                         WdfIoQueueDispatchParallel);  

status = WdfIoQueueCreate(device,  
                          &queueConfig,  
                          WDF_NO_OBJECT_ATTRIBUTES,  
                          &queue);  
 
if (!NT_SUCCESS(status)) {  
     TraceEvents(TRACE_LEVEL_ERROR, DBG_INFO,
                 "Failed to create queue, status=0x%x\n", status);
     goto Done;  
}  

status = WdfObjectAddCustomType(queue, TEST_TYPE1);  

if (!NT_SUCCESS(status)) {  
    TraceEvents(TRACE_LEVEL_ERROR, DBG_INFO,  
                "Failed to add TEST_TYPE1 to WDFOBJECT 0x%p, status=0x%x\n",   
    queue, status);  
    goto Done;  
}    

End:  
    return status;    
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
<td><p>Header</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

