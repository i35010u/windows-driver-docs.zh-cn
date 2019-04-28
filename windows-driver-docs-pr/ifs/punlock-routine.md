---
title: PUNLOCK\_例程函数指针
description: 筛选器 （旧的筛选器或微筛选器） 可以注册 PUNLOCK\_例程类型作为一个文件的筛选器的 UnlockRoutine 回调例程的例程\_锁结构。
ms.assetid: e188bc88-e3dd-49d3-9c79-8eb408cd0338
keywords:
- PUNLOCK_ROUTINE 函数指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- UnlockRoutine
api_location:
- ntifs.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4463eae98b835194329754512cab784cb81601
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352739"
---
# <a name="punlockroutine-function-pointer"></a>PUNLOCK\_例程函数指针


筛选器 （旧的筛选器或微筛选器） 可以注册 PUNLOCK\_作为筛选器的类型化例程的例程*UnlockRoutine*文件的回调例程\_锁结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef VOID ( *UnlockRoutine)(
  _In_ PVOID           Context,
  _In_ PFILE_LOCK_INFO FileLockInfo
);
```

<a name="parameters"></a>Parameters
----------

*上下文*\[中\]  
上下文指针传递给[ **FltProcessFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff543427)或[ **FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)。

*FileLockInfo* \[in\]  
对文件的不透明指针\_锁\_字节范围锁的信息结构。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

筛选器 （旧的筛选器或微筛选器） 可以选择指定 PUNLOCK\_作为筛选器的类型化例程的例程*UnlockRoutine*字节范围文件锁的回调。

如果指定了筛选器*UnlockRoutine*日常文件\_锁结构，此例程称为时从文件中的锁定的字节范围中删除该锁。

微筛选器指定此例程的指针传递给为例程*UnlockRoutine*参数[ **FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)。

旧的筛选器指定此例程的指针传递给为例程*UnlockRoutine*参数[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)或[ **FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)。

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
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff542969)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

[**FltProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543427)

[**FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)

[**FsRtlAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff545640)

[**FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)

[**FsRtlCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545760)

[**FsRtlFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546011)

[**FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)

[**FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)

[**FsRtlUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547313)

[**IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md)

[**PCOMPLETE\_锁\_IRP\_例程**](pcomplete-lock-irp-routine.md)

[**PFLT\_COMPLETE\_LOCK\_CALLBACK\_DATA\_ROUTINE**](https://msdn.microsoft.com/library/windows/hardware/ff551073)

 

 






