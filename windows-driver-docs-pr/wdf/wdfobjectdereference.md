---
title: WdfObjectDereference 宏
description: WdfObjectDereference 宏递减指定框架对象的引用计数。
ms.assetid: e945202c-7e6b-47b7-9216-d7a3a694489e
keywords:
- WdfObjectDereference 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c0766856892b80bd9e870138792ed9f1f5d8414
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823925"
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

*处理*\] 中的 \[  
框架对象的句柄。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供的对象句柄无效，则会发生 bug 检查。

<a name="remarks"></a>备注
-------

如果对象的引用计数变为零，则在**WdfObjectDereference**返回之前可能会删除该对象。

仅当驱动程序之前已调用[**WdfObjectReference**](wdfobjectreference.md)时，才可以调用**WdfObjectDereference** 。

驱动程序可以调用[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)或[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)，而不是调用**WdfObjectDereference**。

有关对象引用计数的详细信息，请参阅[框架对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">全局</a></td>
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
<td><p>标头</p></td>
<td>Wdfobject （包含 Wdf .h）</td>
</tr>
<tr class="odd">
<td><p>库</p></td>
<td>Wdf01000 （KMDF）;WUDFx02000 （UMDF）</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 符合性规则</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate)"><strong>DriverCreate</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla)"><strong>MemAfterReqCompletedIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada)"><strong>MemAfterReqCompletedReadA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea)"><strong>MemAfterReqCompletedWriteA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed" data-raw-source="[&lt;strong&gt;wdfioqueuefindrequestfailed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed)"><strong>wdfioqueuefindrequestfailed</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;wdfioqueueretrievefoundrequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest)"><strong>wdfioqueueretrievefoundrequest</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)

[**WdfObjectReference**](wdfobjectreference.md)

 

 






