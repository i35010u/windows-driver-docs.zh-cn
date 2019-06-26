---
title: WdfObjectReferenceWithTag 宏
description: WdfObjectReferenceWithTag 宏递增指定的 framework 对象的引用计数，并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。
ms.assetid: f0206238-c745-48b3-84d0-9f6d6ec9c2e0
keywords:
- WdfObjectReferenceWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98bad0b0f240ddc155a457e6193a0cc7ae068ab5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354435"
---
# <a name="wdfobjectreferencewithtag-macro"></a>WdfObjectReferenceWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectReferenceWithTag**宏递增指定的 framework 对象的引用计数并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectReferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>Parameters
----------

*处理*\[中\]  
Framework 对象的句柄。

*Tag* \[in\]  
驱动程序定义的一个值，该框架将存储为对象引用的标识标记。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供了无效的对象句柄，则会发生的 bug 检查。

<a name="remarks"></a>备注
-------

如果您的驱动程序调用**WdfObjectReferenceWithTag**递增引用计数，该驱动程序必须调用[ **WdfObjectDereferenceWithTag** ](wdfobjectdereferencewithtag.md)要递减计数。

调用[ **WdfObjectReferenceActual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectreferenceactual)或**WdfObjectReferenceWithTag**而不是[ **WdfObjectReference**](wdfobjectreference.md)向 Microsoft 调试器提供附加信息 （标记值、 行号和文件名称）。 **WdfObjectReferenceActual**允许您的驱动程序指定的行号和文件名称，而**WdfObjectReferenceWithTag**使用驱动程序的当前行号和文件名称。

可以通过查看标记、 行号和文件名称值 **！ wdftagtracker**调试器扩展。 调试器扩展显示为一个指针，以及一系列字符的标记值。 有关调试器扩展的详细信息，请参阅[调试 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)。

有关对象引用计数的详细信息，请参阅[Framework 对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

<a name="examples"></a>示例
--------

下面的代码示例递增对象的引用计数，并将标记值分配给该引用。

```cpp
WdfObjectReferenceWithTag(
                          object,
                          pTag
                          );
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
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WdfObjectReference**](wdfobjectreference.md)

 

 






