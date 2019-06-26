---
title: RxDbgBreakPoint 函数
description: RxDbgBreakPoint 进入内核调试器，如果已安装。
ms.assetid: 981256a4-2faf-4f9e-acfc-7488230bb62e
keywords:
- RxDbgBreakPoint 函数可安装文件系统驱动程序
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
ms.openlocfilehash: a8a1e2147f725299063d4d11fefa18630a07745f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371358"
---
# <a name="rxdbgbreakpoint-function"></a>RxDbgBreakPoint 函数


**RxDbgBreakPoint**进入内核调试器，如果已安装。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID RxDbgBreakPoint(
   ULONG LineNumber
);
```

<a name="parameters"></a>Parameters
----------

*LineNumber*   
源中的行号文件，其中**RxDbgBreakPoint**调用。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程调用内核**DbgBreakPoint**例程。

此例程会引发异常，如果已安装; 由内核调试程序否则可由调试系统进行处理。 如果没有调试器连接到系统，可以采用标准方式处理该异常。

在内核模式下，异常中断处理，则将导致在蓝色屏幕 （bug 检查） 以生成。 但是，可以为已启用内核调试的目标计算机连接内核模式调试程序。 有关详细信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Rxassert.h （包括 Rxassert.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**RxAssert**](rxassert.md)

[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

 

 






