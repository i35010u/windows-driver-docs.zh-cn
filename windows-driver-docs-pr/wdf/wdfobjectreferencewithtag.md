---
title: WdfObjectReferenceWithTag 宏
description: WdfObjectReferenceWithTag 宏会递增指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 宏还向引用分配标记值。
ms.assetid: f0206238-c745-48b3-84d0-9f6d6ec9c2e0
keywords:
- WdfObjectReferenceWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01c72a361c465437036da8e07c640a54d4192ba8
ms.sourcegitcommit: a5f76805387760730faed5674d87201ec85b7dd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90112112"
---
# <a name="wdfobjectreferencewithtag-macro"></a>WdfObjectReferenceWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectReferenceWithTag**宏会递增指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 宏还向引用分配标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectReferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>参数
----------

*句柄* \[中\]  
框架对象的句柄。

*标记* \[中\]  
一个驱动程序定义的值，框架将它存储为对象引用的标识标记。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供的对象句柄无效，则会发生 bug 检查。

<a name="remarks"></a>备注
-------

如果驱动程序调用 **WdfObjectReferenceWithTag** 来递增引用计数，则驱动程序必须调用 [**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md) 来减小计数。

调用 [**WdfObjectReferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual) 或 **WdfObjectReferenceWithTag** 而不是 [**WdfObjectReference**](wdfobjectreference.md) 将 (标记值、行号和文件名) 的其他信息提供给 Microsoft 调试器。 **WdfObjectReferenceActual** 允许驱动程序指定行号和文件名，而 **WdfObjectReferenceWithTag** 使用驱动程序的当前行号和文件名。

可以通过使用 **！ wdftagtracker** 调试器扩展来查看标记、行号和文件名值。 调试器扩展将标记值显示为指针和一系列字符。 有关调试器扩展的详细信息，请参阅 [调试 KMDF 驱动程序](../debugger/kernel-mode-driver-framework-debugging.md)。

有关对象引用计数的详细信息，请参阅 [框架对象生命周期](./framework-object-life-cycle.md)。

<a name="examples"></a>示例
--------

下面的代码示例将增加一个对象的引用计数，并为该引用分配一个标记值。

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
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WdfObjectReference**](wdfobjectreference.md)

 

