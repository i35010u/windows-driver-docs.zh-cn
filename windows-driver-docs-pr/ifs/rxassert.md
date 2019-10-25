---
title: RxAssert 例程
description: 如果安装了 RxAssert，则在已安装的 RDBSS 版本上，会将断言字符串发送到内核调试器。 对于 RDBSS 的零售版本，对此例程的调用将进行 bug 检查。
ms.assetid: 3ef01569-74ef-4f35-acaf-9c01f2b9d9a7
keywords:
- RxAssert 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- RxAssert
api_location:
- rxassert.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7ef93d1ad010614582d93016a5bc2be761f5012
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840977"
---
# <a name="rxassert-routine"></a>RxAssert 例程


如果安装了 RxAssert，则在已安装的 RDBSS 版本上，会将断言字符串发送到内核调试器。 对于 RDBSS 的零售版本，对此例程的调用将进行 bug 检查。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID RxAssert(
  _In_     PVOID FailedAssertion,
  _In_     PVOID FileName,
  _In_     ULONG LineNumber,
  _In_opt_ PCHAR Message
);
```

<a name="parameters"></a>参数
----------

\] 中的*FailedAssertion* \[  
失败的断言。

*文件名*\[\]  
调用**RxAssert**或**RtlAssert**的源文件的名称。

\] 中的*LineNumber* \[  
源文件中调用了**RxAssert**或**RtlAssert**的行号。

*消息*\[in，可选\]  
可选消息。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

使用*rxassert*包含文件时，将重新定义 Windows 内核 RtlAssert 调用以调用此 rxassert 例程。

在零售版本中， **RxAssert**将调用**KeBugCheckEx**值0xa55a0000 运算中的值，并将行号作为 BugCheckParamater1。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Rxassert （包括 Rxassert）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**断言**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))

[RtlAssert](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**RxDbgBreakPoint**](rxdbgbreakpoint.md)

 

 






