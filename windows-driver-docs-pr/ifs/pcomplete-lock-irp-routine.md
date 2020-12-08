---
title: PCOMPLETE \_ LOCK \_ IRP \_ 例程例程
description: 文件系统筛选器驱动程序 (旧筛选器) 可以 \_ 将 PCOMPLETE LOCK \_ IRP \_ 例程类型例程注册为筛选器的 CompleteLockIrpRoutine 回调。
keywords:
- CompleteLockIrpRoutine 例程可安装文件系统驱动程序
- PCOMPLETE_LOCK_IRP_ROUTINE
topic_type:
- apiref
api_name:
- CompleteLockIrpRoutine
api_location:
- ntifs.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230379d193a191a3ab24a0946e5a559ce3d71d90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816263"
---
# <a name="pcomplete_lock_irp_routine-routine"></a>PCOMPLETE \_ LOCK \_ IRP \_ 例程例程


文件系统筛选器驱动程序 (旧筛选器) 可以 \_ 将 PCOMPLETE LOCK \_ IRP \_ 例程类型例程注册为筛选器的 *CompleteLockIrpRoutine* 回调。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PCOMPLETE_LOCK_IRP_ROUTINE CompleteLockIrpRoutine;

NTSTATUS CompleteLockIrpRoutine(
  _In_ PVOID Context,
  _In_ PIRP  Irp
)
{ ... }
```

<a name="parameters"></a>参数
----------

*上下文* \[中\]  
传递给 [**FsRtlProcessFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)的上下文指针。

*Irp* \[中\]  
用于文件锁定 [**irp \_ MJ \_ 锁定 \_ 控制**](irp-mj-lock-control.md) 请求的 irp 正在完成。 锁定请求类型将为以下类型之一：

IRP \_ MN \_ 锁

IRP \_ MN \_ \_ 全部解锁

IRP \_ MN \_ \_ \_ 按密钥解锁 \_

IRP \_ MN \_ \_

<a name="return-value"></a>返回值
------------

此例程返回状态 \_ 成功或适当的 NTSTATUS 值。 如果它返回不是成功代码的 NTSTATUS 值，则将从文件中删除该文件锁。

<a name="remarks"></a>备注
-------

 (旧版筛选器的文件系统筛选器驱动程序) 可以选择指定 PCOMPLETE \_ 锁 \_ IRP \_ 例程类型例程作为旧筛选器的 *CompleteLockIrpRoutine* 例程，用于字节范围文件锁定。

若要指定此例程，旧版筛选器会将例程的指针传递为 [**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)或 [**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)的 *CompleteLockIrpRoutine* 参数。

如果旧筛选器为文件锁指定了 *CompleteLockIrpRoutine* 例程，则系统会在为文件锁定完成 [**IRP \_ MJ \_ 锁定 \_ 控制**](irp-mj-lock-control.md) 操作时调用此例程。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP \_ MJ \_ 锁定 \_ 控制**](irp-mj-lock-control.md)

[**PUNLOCK \_ 例程**](punlock-routine.md)

 

