---
title: WdfObjectReference 宏
description: WdfObjectReference 宏递增指定的 framework 对象的引用计数。
ms.assetid: 8e024197-d366-4665-994b-4e03f559e017
keywords:
- WdfObjectReference 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c463251e8282189c9c9b6de92cb346dba81f4f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385734"
---
# <a name="wdfobjectreference-macro"></a>WdfObjectReference 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectReference**宏递增指定的 framework 对象的引用计数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectReference(
  [in] WDFOBJECT Handle
);
```

<a name="parameters"></a>Parameters
----------

*处理*\[中\]  
Framework 对象的句柄。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供了无效的对象句柄，则会发生的 bug 检查。

<a name="remarks"></a>备注
-------

如果您的驱动程序调用**WdfObjectReference**递增引用计数，该驱动程序必须调用[ **WdfObjectDereference** ](wdfobjectdereference.md)要递减计数。

而不是调用**WdfObjectReference**，驱动程序可以调用[ **WdfObjectReferenceWithTag** ](wdfobjectreferencewithtag.md)或者[ **WdfObjectReferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548760).

有关对象引用计数的详细信息，请参阅[Framework 对象生命周期](https://msdn.microsoft.com/library/windows/hardware/ff542889)。

<a name="examples"></a>示例
--------

下面的代码示例递增对象的引用计数。

```cpp
WdfObjectReference(Object); 
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
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h （包括 Wdf.h）</td>
</tr>
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF); WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff544957" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544957)"><strong>DriverCreate</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff549090" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549090)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff549106" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549106)"><strong>MemAfterReqCompletedIoctlA</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff549116" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549116)"><strong>MemAfterReqCompletedReadA</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff549125" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549125)"><strong>MemAfterReqCompletedWriteA</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WdfObjectReferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548760)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

 






