---
title: WdfObjectDereference 宏
description: WdfObjectDereference 宏递减指定框架对象的引用计数。
ms.assetid: e945202c-7e6b-47b7-9216-d7a3a694489e
keywords:
- WdfObjectDereference 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0630541ab4ef06b6933da336701c5080eeee544
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105254"
---
# <a name="wdfobjectdereference-macro"></a>WdfObjectDereference 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectDereference**宏递减指定框架对象的引用计数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectDereference(
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

<a name="remarks"></a>备注
-------

如果对象的引用计数变为零，则在 **WdfObjectDereference** 返回之前可能会删除该对象。

仅当驱动程序之前已调用[**WdfObjectReference**](wdfobjectreference.md)时，才可以调用**WdfObjectDereference** 。

驱动程序可以调用[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)或[**WdfObjectDereferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)，而不是调用**WdfObjectDereference**。

有关对象引用计数的详细信息，请参阅 [框架对象生命周期](./framework-object-life-cycle.md)。

<a name="examples"></a>示例
--------

下面的代码示例减小了对象的引用计数。

```cpp
WdfObjectDereference(Object); 
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
<td><a href="/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](../devtest/kmdf-drivercreate.md)"><strong>DriverCreate</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](../devtest/kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed" data-raw-source="[&lt;strong&gt;wdfioqueuefindrequestfailed&lt;/strong&gt;](../devtest/kmdf-wdfioqueuefindrequestfailed.md)"><strong>wdfioqueuefindrequestfailed</strong></a>、 <a href="/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;wdfioqueueretrievefoundrequest&lt;/strong&gt;](../devtest/kmdf-wdfioqueueretrievefoundrequest.md)"><strong>wdfioqueueretrievefoundrequest</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WdfObjectDereferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)

[**WdfObjectReference**](wdfobjectreference.md)

