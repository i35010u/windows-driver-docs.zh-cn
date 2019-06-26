---
title: WdfObjectAddCustomType 宏
description: WdfObjectAddCustomType 宏将 framework 对象与自定义类型相关联。
ms.assetid: 750CF669-A436-4571-B474-D5447E0AA64F
keywords:
- WdfObjectAddCustomType 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fe421c1173819cf2f810334b274eb9b467a7658
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372106"
---
# <a name="wdfobjectaddcustomtype-macro"></a>WdfObjectAddCustomType 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectAddCustomType**宏将 framework 对象与自定义类型相关联。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomType(
    _handle,
    _type
);
```

<a name="parameters"></a>Parameters
----------

*_handle*   
Framework 对象的句柄。

*_type*   
自定义类型的驱动程序定义名称。

<a name="return-value"></a>返回值
------------

**WdfObjectAddCustomType**返回 STATUS_SUCCESS，如果操作成功。 否则，此方法可能返回以下值之一：

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
<td><p>指定句柄不能具有自定义类型添加到它。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td><p>未能分配自定义的类型。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_OBJECT_NAME_EXISTS</strong></td>
<td><p>该驱动程序已添加指定的自定义类型。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_DELETE_PENDING</strong></td>
<td><p>正在删除句柄参数指定的对象。 在此情况下，该框架不会添加自定义的类型。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**WdfObjectAddCustomType**是一个简化的版的[ **WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)。

有关对象驱动程序类型的详细信息，请参阅[Framework 对象自定义类型](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-custom-types)。

<a name="examples"></a>示例
--------

此示例代码演示如何将自定义类型添加到队列。

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

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 






