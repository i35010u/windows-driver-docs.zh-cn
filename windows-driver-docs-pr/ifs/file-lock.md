---
title: FILE_LOCK 结构
description: 操作系统使用不透明的文件 \_ 锁定结构来支持文件锁定。
ms.assetid: 89df2075-c542-4105-847f-9bc7ae4dab50
keywords:
- FILE_LOCK 结构可安装文件系统驱动程序
- PFILE_LOCK 结构指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FILE_LOCK
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e289b2a24ca49e2e776fc4b4bc1b3597d10581e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063686"
---
# <a name="file_lock-structure"></a>文件 \_ 锁定结构


操作系统使用不透明的文件 \_ 锁定结构来支持文件锁定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _FILE_LOCK {
  PCOMPLETE_LOCK_IRP_ROUTINE CompleteLockIrpRoutine;
  PUNLOCK_ROUTINE            UnlockRoutine;
  BOOLEAN                    FastIoIsQuestionable;
  BOOLEAN                    SpareC[3];
  PVOID                      LockInformation;
  FILE_LOCK_INFO             LastReturnedLockInfo;
  PVOID                      LastReturnedLock;
  volatile LONG              LockRequestsInProgress;
} FILE_LOCK, *PFILE_LOCK;
```

<a name="members"></a>成员
-------

**CompleteLockIrpRoutine**  
预留给系统使用。

**UnlockRoutine**  
预留给系统使用。

**FastIoIsQuestionable**  
预留给系统使用。

**SpareC**  
预留给系统使用。

**LockInformation**  
预留给系统使用。

**LastReturnedLockInfo**  
预留给系统使用。

**LastReturnedLock**  
预留给系统使用。

**LockRequestsInProgress**  
预留给系统使用。

<a name="remarks"></a>备注
-------

文件系统驱动程序、旧的文件系统筛选器驱动程序和 minifilters 可以使用各种例程来创建和使用文件 \_ 锁定对象，并测试文件的读/写访问权限。

-   若要分配文件 \_ 锁定对象，请调用 [**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock) 或 [**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)。

-   若要初始化未初始化的文件 \_ 锁定对象，请调用 [**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock) 或 [**FltInitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)。 请注意， \_ 从 [**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock) 或 [**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock) 返回的文件锁定已初始化。

-   若要取消对文件 \_ 锁定对象的初始化，请调用 [**FsRtlUninitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock) 或 [**FltUninitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)。

-   若要释放 \_ [**FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock) 例程分配的文件锁定对象，请调用 [**FsRtlFreeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)。 若要释放 \_ [**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock) 例程分配的文件锁定对象，请调用 [**FltFreeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)。

文件 \_ 锁初始化完成后，可使用 [**FsRtlCheckLockForReadAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)、 [**FltCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)和 [**FsRtlFastCheckLockForRead**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread) 等例程来确定文件是否可由其他线程访问。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 FltKernel 或 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltInitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

**FltInitializeFileLock** 
[ **FsRtlAllocateFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFastCheckLockForRead**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread)

[**FsRtlFastCheckLockForWrite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforwrite)

[**FsRtlInitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlUninitializeFileLock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

 

