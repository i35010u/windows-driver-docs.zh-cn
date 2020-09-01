---
title: CcSetLogHandleForFileEx 例程
description: CcSetLogHandleForFileEx 例程为文件设置日志句柄并跟踪文件日志的回调函数。
ms.assetid: D56BEAC9-6AB8-44BA-ADFC-D2435A1458DB
keywords:
- CcSetLogHandleForFileEx 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcSetLogHandleForFileEx
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f9943bb14565e88b5feff39199a3943a885fabd
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065358"
---
# <a name="ccsetloghandleforfileex-routine"></a>CcSetLogHandleForFileEx 例程


**CcSetLogHandleForFileEx**例程为文件设置日志句柄并跟踪文件日志的回调函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcSetLogHandleForFileEx(
  _In_ PFILE_OBJECT     FileObject,
  _In_ PVOID            LogHandle,
  _In_ PFLUSH_TO_LSN    FlushToLsnRoutine,
  _In_ PQUERY_LOG_USAGE QueryLogUsageRoutine
);
```

<a name="parameters"></a>parameters
----------

*FileObject* \[\]，它指向要存储日志句柄的文件的文件对象。

*LogHandle* \[指向要 \] 存储的日志句柄的指针。

*FlushToLsnRoutine* \[指向 \] 日志文件的指针刷新回调例程，以便在刷新此文件的缓冲区之前调用。 此例程用于确保将日志文件刷新到任何缓冲区控制块 (LSN) 的最新逻辑序列号， (正在刷新的 BCB) 。 此例程声明如下：

```cpp
typedef
VOID (*PFLUSH_TO_LSN) (
            IN PVOID LogHandle,
            IN LARGE_INTEGER Lsn
            );
```

<a href="" id="loghandle"></a>
***LogHandle***

一个指针，指向用于标识此客户端的不透明结构。

<a href="" id="lsn"></a>
***Lsn***

这是在从此回调例程返回时磁盘上必须有的 LSN。

*QueryLogUsageRoutine* \[指向用于 \] 检索此文件的日志用量百分比的客户端回调例程的指针。 调用此例程来检查是否满足阈值来启动写入脏页。 此例程声明如下：

```cpp
typedef  
VOID (*PQUERY_LOG_USAGE) (  
            IN PVOID LogHandle,  
            OUT PUSHORT PercentageFull  
            );  
```

<a href="" id="loghandle"></a>
***LogHandle***

一个指针，指向用于标识此客户端的不透明结构。

<a href="" id="percentagefull"></a>
***PercentageFull***

一个介于0到100之间的值，用于指示日志使用的百分比。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**CcSetLogHandleForFileEx** 设置文件的日志句柄，以便在对 [**CcGetDirtyPages**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccgetdirtypages)的后续调用中使用。

*FlushToLsnRoutine*和*QueryLogUsageRoutine*的回调是必需的。 这些值不得为 NULL。

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
<td align="left"><p>在 Windows 8 及更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs) </td>
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
<td align="left"><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CcGetDirtyPages**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccgetdirtypages)

[**CcSetDirtyPinnedData**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccsetdirtypinneddata)

 

