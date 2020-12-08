---
title: PUNLOCK \_ 例程函数指针
description: 筛选器 (旧筛选器或微筛选器) 可以将 PUNLOCK \_ 例程类型化例程注册为文件锁结构的筛选器 UnlockRoutine 回调例程 \_ 。
keywords:
- PUNLOCK_ROUTINE 函数指针可安装的文件系统驱动程序
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
ms.openlocfilehash: 4bb3b4f1d4fe10cdc4ee78432a59a5c72093b537
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838601"
---
# <a name="punlock_routine-function-pointer"></a>PUNLOCK \_ 例程函数指针


筛选器 (旧筛选器或微筛选器) 可以将 PUNLOCK \_ 例程类型化例程注册为文件锁结构的筛选器 *UnlockRoutine* 回调例程 \_ 。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef VOID ( *UnlockRoutine)(
  _In_ PVOID           Context,
  _In_ PFILE_LOCK_INFO FileLockInfo
);
```

<a name="parameters"></a>参数
----------

*上下文* \[中\]  
传递给 [**FltProcessFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock) 或 [**FsRtlProcessFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)的上下文指针。

*FileLockInfo* \[中\]  
指向 \_ 字节范围锁的文件锁信息结构的不透明指针 \_ 。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

筛选器 (旧版筛选器或微筛选器) 可以选择将 PUNLOCK \_ 例程类型化例程指定为字节范围文件锁的筛选器 *UnlockRoutine* 回调。

如果筛选器为文件锁结构指定 *UnlockRoutine* 例程 \_ ，则在从文件中的锁定字节范围内删除该锁时，将调用此例程。

微筛选器通过将指向例程的指针作为 [**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)的 *UnlockRoutine* 参数进行传递来指定此例程。

旧筛选器通过将指向例程的指针作为 [**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)或 [**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)的 *UnlockRoutine* 参数进行传递来指定此例程。

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
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP \_ MJ \_ 锁定 \_ 控制**](irp-mj-lock-control.md)

[**PCOMPLETE \_ LOCK \_ IRP \_ 例程**](pcomplete-lock-irp-routine.md)

[**PFLT \_ 完成 \_ 锁定 \_ 回调 \_ 数据 \_ 例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

 

