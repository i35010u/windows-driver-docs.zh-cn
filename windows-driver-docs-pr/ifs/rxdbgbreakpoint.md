---
title: RxDbgBreakPoint 函数
description: 如果安装了一个，RxDbgBreakPoint 将中断内核调试器。
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
ms.openlocfilehash: 114ec581a7d586db459bcbd8abe3f2c3ffd8d01d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789917"
---
# <a name="rxdbgbreakpoint-function"></a>RxDbgBreakPoint 函数


如果安装了一个， **RxDbgBreakPoint** 将中断内核调试器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID RxDbgBreakPoint(
   ULONG LineNumber
);
```

<a name="parameters"></a>参数
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
<td align="left">台式机</td>
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

## <a name="see-also"></a>请参阅


[**RxAssert**](rxassert.md)

[Windows 调试](../debugger/index.md)

 

