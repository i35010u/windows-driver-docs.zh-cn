---
title: PCOMPLETE\_锁\_IRP\_例程例程
description: 文件系统筛选器驱动程序 （旧筛选器） 可以注册 PCOMPLETE\_锁\_IRP\_作为筛选器的 CompleteLockIrpRoutine 回调例程类型化的例程。
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
ms.openlocfilehash: bfcbe5acc8aa646816652cd9e5c2ec153eeaecd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386064"
---
# <a name="pcompletelockirproutine-routine"></a>PCOMPLETE\_锁\_IRP\_例程例程


文件系统筛选器驱动程序 （旧筛选器） 可以注册 PCOMPLETE\_锁\_IRP\_作为筛选器的类型化例程的例程*CompleteLockIrpRoutine*回调。

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

<a name="parameters"></a>Parameters
----------

*上下文*\[中\]  
上下文指针传递给[ **FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)。

*Irp* \[中\]  
文件锁的 IRP [ **IRP\_MJ\_锁\_控制**](irp-mj-lock-control.md)为正在完成的请求。 锁请求类型将是以下之一：

IRP\_MN\_锁

IRP\_MN\_解锁\_所有

IRP\_MN\_解锁\_所有\_BY\_密钥

IRP\_MN\_解锁\_单一

<a name="return-value"></a>返回值
------------

此例程将返回状态\_成功或适当的 NTSTATUS 值。 如果它返回 NTSTATUS 值不是一个成功代码，从文件中删除文件锁定。

<a name="remarks"></a>备注
-------

文件系统筛选器驱动程序 （旧筛选器） 可以选择指定 PCOMPLETE\_锁\_IRP\_例程类型为旧的筛选器的例程*CompleteLockIrpRoutine*的例程字节范围文件锁定。

若要指定此例程，旧的筛选器将指针传递到作为例程*CompleteLockIrpRoutine*参数[ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)或[ **FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)。

如果旧的筛选器指定了*CompleteLockIrpRoutine*日常文件锁，系统将调用此例程完成时[ **IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md)文件锁的操作。

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
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md)

[**PUNLOCK\_例程**](punlock-routine.md)

 

 






