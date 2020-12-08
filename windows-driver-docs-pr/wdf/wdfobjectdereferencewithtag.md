---
title: WdfObjectDereferenceWithTag 宏
description: WdfObjectDereferenceWithTag 宏递减指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 此宏还向引用分配标记值。
keywords:
- WdfObjectDereferenceWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06759538b46367722c67ea05a17ded0d622be227
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809763"
---
# <a name="wdfobjectdereferencewithtag-macro"></a>WdfObjectDereferenceWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectDereferenceWithTag** 宏递减指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 此宏还向引用分配标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectDereferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>参数
----------

*句柄* \[中\]  
框架对象的句柄。

*标记* \[中\]  
用于标识对象引用的驱动程序定义的值。 标记值必须匹配驱动程序以前提供给 [**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)的标记值。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供的对象句柄无效，则会发生 bug 检查。

<a name="remarks"></a>备注
-------

如果对象的引用计数变为零，则在 **WdfObjectDereferenceWithTag** 返回之前可能会删除该对象。

调用 [**WdfObjectDereferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual) 或 **WdfObjectDereferenceWithTag** 而不是 [**WdfObjectDereference**](wdfobjectdereference.md) (标记字符串、行号和文件名) Microsoft 调试器提供附加信息。 **WdfObjectDereferenceActual** 允许驱动程序指定行号和文件名，而 **WdfObjectDereferenceWithTag** 使用驱动程序的当前行号和文件名。

可以通过使用 **！ wdftagtracker** 调试器扩展来查看标记、行号和文件名值。 调试器扩展将标记值显示为指针和一系列字符。 有关调试器扩展的详细信息，请参阅 [调试 KMDF 驱动程序](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。

有关对象引用计数的详细信息，请参阅 [框架对象生命周期](./framework-object-life-cycle.md)。

<a name="examples"></a>示例
--------

下面的代码示例将减小对象的引用计数，并为引用分配标记值。

```cpp
WdfObjectDereferenceWithTag(
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

## <a name="see-also"></a>请参阅


[**WdfObjectDereference**](wdfobjectdereference.md)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

