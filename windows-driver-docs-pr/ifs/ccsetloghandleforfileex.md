---
title: CcSetLogHandleForFileEx routine
description: CcSetLogHandleForFileEx 例程设置的日志句柄的文件和跟踪的回调函数的文件日志。
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
ms.openlocfilehash: f0709e0223fdf6ab65bcf094792ebeaf361666fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352197"
---
# <a name="ccsetloghandleforfileex-routine"></a>CcSetLogHandleForFileEx routine


**CcSetLogHandleForFileEx**例程设置的日志句柄的文件和跟踪的回调函数的文件日志。

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

<a name="parameters"></a>Parameters
----------

*文件对象*\[中\]指向将存储日志句柄的文件的文件对象。

*LogHandle* \[中\]指针，指向要存储的日志句柄。

*FlushToLsnRoutine* \[中\]指向日志文件刷新之前刷新此文件的缓冲区调用的回调例程。 此例程称为以确保刷新任何缓冲区控制块 (BCB) 的日志文件刷新到最新的逻辑序列号 (LSN)。 此例程声明，如下所示：

```cpp
typedef
VOID (*PFLUSH_TO_LSN) (
            IN PVOID LogHandle,
            IN LARGE_INTEGER Lsn
            );
```

<a href="" id="loghandle"></a>
***LogHandle***

指向用来标识此客户端的不透明结构。

<a href="" id="lsn"></a>
***Lsn***

这是必须在磁盘上在该回调例程中返回的 LSN。

*QueryLogUsageRoutine* \[中\]指向客户端的回调例程调用来检索此文件的日志使用率的百分比。 此例程调用以检查是否达到阈值时启动的脏页写入。 此例程声明，如下所示：

```cpp
typedef  
VOID (*PQUERY_LOG_USAGE) (  
            IN PVOID LogHandle,  
            OUT PUSHORT PercentageFull  
            );  
```

<a href="" id="loghandle"></a>
***LogHandle***

指向用来标识此客户端的不透明结构。

<a href="" id="percentagefull"></a>
***PercentageFull***

介于 0 到 100，该值指示日志使用率的百分比。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

**CcSetLogHandleForFileEx**设置文件，以便在后续调用中使用的日志句柄[ **CcGetDirtyPages**](https://msdn.microsoft.com/library/windows/hardware/ff539088)。

回叫*FlushToLsnRoutine*并*QueryLogUsageRoutine*所需。 这些值不能为 NULL。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>适用于 Windows 8 及更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
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

## <a name="see-also"></a>请参阅


[**CcGetDirtyPages**](https://msdn.microsoft.com/library/windows/hardware/ff539088)

[**CcSetDirtyPinnedData**](https://msdn.microsoft.com/library/windows/hardware/ff539211)

 

 






