---
title: PCOMPLETE\_锁定\_IRP\_例程例程
description: 文件系统筛选器驱动程序（旧筛选器）可以将 PCOMPLETE\_锁定\_IRP\_例程类型例程注册为筛选器的 CompleteLockIrpRoutine 回调。
ms.assetid: 400ff351-5906-4e6e-a708-e71441afe3b8
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
ms.openlocfilehash: 4dfa49f57d705f42176307686debca2939c61daf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841041"
---
# <a name="pcomplete_lock_irp_routine-routine"></a>PCOMPLETE\_锁定\_IRP\_例程例程


文件系统筛选器驱动程序（旧筛选器）可以将 PCOMPLETE\_锁定\_IRP\_例程类型例程注册为筛选器的*CompleteLockIrpRoutine*回调。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PCOMPLETE_LOCK_IRP_ROUTINE CompleteLockIrpRoutine;

NTSTATUS CompleteLockIrpRoutine(
  _In_ PVOID Context,
  _In_ PIRP  Irp
)
{ ... }
```

<a name="parameters"></a>参数
----------

*上下文*\[\]  
传递给[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)的上下文指针。

*Irp* \[\]  
文件锁定 Irp 的 IRP [ **\_MJ\_锁定**](irp-mj-lock-control.md)要完成的\_控制请求。 锁定请求类型将为以下类型之一：

IRP\_MN\_锁定

IRP\_MN\_解锁\_

IRP\_MN\_通过\_密钥\_所有\_进行解锁

IRP\_MN\_解锁\_单一

<a name="return-value"></a>返回值
------------

此例程返回状态\_SUCCESS 或适当的 NTSTATUS 值。 如果它返回不是成功代码的 NTSTATUS 值，则将从文件中删除该文件锁。

<a name="remarks"></a>备注
-------

文件系统筛选器驱动程序（旧筛选器）可以根据需要指定 PCOMPLETE\_锁\_IRP\_例程类型例程，作为字节范围文件锁的旧筛选器的*CompleteLockIrpRoutine*例程。

若要指定此例程，旧版筛选器会将例程的指针传递为[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)或[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)的*CompleteLockIrpRoutine*参数。

如果旧筛选器为文件锁指定了*CompleteLockIrpRoutine*例程，则系统会在完成[**IRP\_MJ\_锁定文件锁定\_控制**](irp-mj-lock-control.md)操作时调用此例程。

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
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_锁定\_控件**](irp-mj-lock-control.md)

[**PUNLOCK\_例程**](punlock-routine.md)

 

 






