---
title: RxAssert 例程
description: RxAssert 发送上选中的 ASSERT 字符串生成的 RDBSS 到内核调试程序如果安装了一个。 对于零售版本的 RDBSS，对此例程的调用将 bug 检查。
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
ms.openlocfilehash: 4acca9a3a22ba85bcfd529a8555f8eec4e0adbf0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385032"
---
# <a name="rxassert-routine"></a>RxAssert 例程


**RxAssert**的 RDBSS checked 版本为 ASSERT 字符串发送到内核调试程序，如果安装了一个。 对于零售版本的 RDBSS，对此例程的调用将 bug 检查。

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

<a name="parameters"></a>Parameters
----------

*FailedAssertion* \[in\]  
失败的断言。

*FileName* \[in\]  
文件的源的名称，其中**RxAssert**或**RtlAssert**调用。

*LineNumber* \[in\]  
源中的行号文件，其中**RxAssert**或**RtlAssert**调用。

*消息* \[in，可选\]  
可选的消息。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

当*rxassert.h*包括使用文件时，将重新定义 Windows 内核 RtlAssert 调用以调用此的 RxAssert 例程。

在零售版本中， **RxAssert**将调用**KeBugCheckEx**传入值 0xa55a0000 作为 BugCheckParamater1 的行号或运算。

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


[**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))

[RtlAssert](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**RxDbgBreakPoint**](rxdbgbreakpoint.md)

 

 






