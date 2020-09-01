---
title: RxDbgBreakPoint 函数
description: 如果安装了一个，RxDbgBreakPoint 将中断内核调试器。
ms.assetid: 981256a4-2faf-4f9e-acfc-7488230bb62e
keywords:
- RxDbgBreakPoint 函数可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- RxDbgBreakPoint
api_location:
- rxassert.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28169d0b0b7a19741dfb4b19f0bcab4f8607c780
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067364"
---
# <a name="rxdbgbreakpoint-function"></a>RxDbgBreakPoint 函数


如果安装了一个， **RxDbgBreakPoint**将中断内核调试器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID RxDbgBreakPoint(
   ULONG LineNumber
);
```

<a name="parameters"></a>parameters
----------

*LineNumber*   
源文件中调用 **RxDbgBreakPoint** 的行号。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程调用内核 **DbgBreakPoint** 例程。

如果安装了某个内核调试器，此例程会引发异常;否则，调试系统会对其进行处理。 如果没有任何调试器连接到系统，则可以采用标准方式处理异常。

在内核模式下，未处理的中断异常将导致蓝屏 (bug 检查) 结果。 但是，可以将内核模式调试器连接到已启用内核调试的目标计算机。 有关详细信息，请参阅 [Windows 调试](../debugger/index.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Rxassert (包含 Rxassert) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**RxAssert**](rxassert.md)

[Windows 调试](../debugger/index.md)

 

