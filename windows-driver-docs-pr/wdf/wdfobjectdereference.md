---
title: WdfObjectDereference 宏
description: WdfObjectDereference 宏递减指定的 framework 对象的引用计数。
ms.assetid: e945202c-7e6b-47b7-9216-d7a3a694489e
keywords:
- WdfObjectDereference 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33a709b437c9e3606a76a9c789dac74881cce3e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372087"
---
# <a name="wdfobjectdereference-macro"></a>WdfObjectDereference 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectDereference**宏递减引用计数为指定的框架对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectDereference(
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

如果该对象的引用计数变为零，对象可能被删除之前**WdfObjectDereference**返回。

驱动程序可以调用**WdfObjectDereference**仅当它以前被称为[ **WdfObjectReference**](wdfobjectreference.md)。

而不是调用**WdfObjectDereference**，驱动程序可以调用[ **WdfObjectDereferenceWithTag** ](wdfobjectdereferencewithtag.md)或者[ **WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)。

有关对象引用计数的详细信息，请参阅[Framework 对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

<a name="examples"></a>示例
--------

以下代码示例递减对象的引用计数。

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate)"><strong>DriverCreate</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla)"> <strong>MemAfterReqCompletedIntIoctlA</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla)"> <strong>MemAfterReqCompletedIoctlA</strong></a>，<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada)"> <strong>MemAfterReqCompletedReadA</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea)"> <strong>MemAfterReqCompletedWriteA</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed" data-raw-source="[&lt;strong&gt;wdfioqueuefindrequestfailed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed)"> <strong>wdfioqueuefindrequestfailed</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;wdfioqueueretrievefoundrequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest)"> <strong>wdfioqueueretrievefoundrequest</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)

[**WdfObjectReference**](wdfobjectreference.md)

 

 






