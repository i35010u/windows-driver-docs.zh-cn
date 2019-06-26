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
ms.openlocfilehash: b6b2a17e00b62e20983b31336667888de6bd25cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385146"
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
上下文指针传递给[ **FltProcessFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)或[ **FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)。

*FileLockInfo* \[in\]  
对文件的不透明指针\_锁\_字节范围锁的信息结构。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

筛选器 （旧的筛选器或微筛选器） 可以选择指定 PUNLOCK\_作为筛选器的类型化例程的例程*UnlockRoutine*字节范围文件锁的回调。

如果指定了筛选器*UnlockRoutine*日常文件\_锁结构，此例程称为时从文件中的锁定的字节范围中删除该锁。

微筛选器指定此例程的指针传递给为例程*UnlockRoutine*参数[ **FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)。

旧的筛选器指定此例程的指针传递给为例程*UnlockRoutine*参数[ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)或[ **FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)。

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


[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md)

[**PCOMPLETE\_锁\_IRP\_例程**](pcomplete-lock-irp-routine.md)

[**PFLT\_COMPLETE\_LOCK\_CALLBACK\_DATA\_ROUTINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

 

 






