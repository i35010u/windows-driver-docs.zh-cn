---
title: CcSetLoggedDataThreshold 例程
description: 当对脏日志页的扫描将启动延迟写入时，CcSetLoggedDataThreshold 例程将设置阈值。
keywords:
- CcSetLoggedDataThreshold 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcSetLoggedDataThreshold
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eade8f3f180cf531b043f8e82cdcff7e96000948
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788723"
---
# <a name="ccsetloggeddatathreshold-routine"></a>CcSetLoggedDataThreshold 例程


当对脏日志页的扫描将启动延迟写入时， [**CcSetLoggedDataThreshold**](ccistheredirtyloggedpages.md) 例程将设置阈值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcSetLoggedDataThreshold(
  _In_ PVOID LogHandle,
  _In_ ULONG NumberOfPages
);
```

<a name="parameters"></a>参数
----------

*LogHandle* \[中\]  
新阈值的日志句柄。

*NumberOfPages* \[中\]  
*LogHandle* 指定的日志的脏日志页中的阈值号。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

仅当 *QueryLogUsageRoutine* 回调例程的 *PercentageUsed* 参数中返回的值为0时，才使用 *NumberOfPages* 中的阈值。 使用对 [**CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)的调用设置 *QueryLogUsageRoutine* 回调。

当未使用日志完整百分比时， [**CcSetLoggedDataThreshold**](ccistheredirtyloggedpages.md) 例程用于在脏日志页的数量中设置固定值。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 FltKernel) </td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)

 

 






