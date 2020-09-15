---
title: WdfObjectReference 宏
description: WdfObjectReference 宏会递增指定框架对象的引用计数。
ms.assetid: 8e024197-d366-4665-994b-4e03f559e017
keywords:
- WdfObjectReference 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5120b0ddbc7e59465fe0ddc69014036d33b10963
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106532"
---
# <a name="wdfobjectreference-macro"></a>WdfObjectReference 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectReference**宏会递增指定框架对象的引用计数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectReference(
  [in] WDFOBJECT Handle
);
```

<a name="parameters"></a>参数
----------

*句柄* \[中\]  
框架对象的句柄。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供的对象句柄无效，则会发生 bug 检查。

<a name="remarks"></a>注解
-------

如果驱动程序调用 **WdfObjectReference** 来递增引用计数，则驱动程序必须调用 [**WdfObjectDereference**](wdfobjectdereference.md) 来减小计数。

驱动程序可以调用[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)或[**WdfObjectReferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)，而不是调用**WdfObjectReference**。

有关对象引用计数的详细信息，请参阅 [框架对象生命周期](./framework-object-life-cycle.md)。

<a name="examples"></a>示例
--------

下面的代码示例将增加对象的引用计数。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
<tr class="odd">
<td><p>库</p></td>
<td>Wdf01000.sys (KMDF) ;WUDFx02000.dll (UMDF) </td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](../devtest/kmdf-drivercreate.md)"><strong>DriverCreate</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WdfObjectReferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

