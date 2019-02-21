---
title: FILE_LOCK 结构
description: 操作系统使用的不透明文件\_锁结构，以支持的文件锁定。
ms.assetid: 89df2075-c542-4105-847f-9bc7ae4dab50
keywords:
- FILE_LOCK 结构可安装文件系统驱动程序
- PFILE_LOCK 结构指针可安装文件系统驱动程序
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
ms.openlocfilehash: 091012d1d2732cba714711dd40af56f34e203f2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522477"
---
# <a name="filelock-structure"></a>文件\_锁结构


操作系统使用的不透明文件\_锁结构，以支持的文件锁定。

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
保留供系统使用。

**UnlockRoutine**  
保留供系统使用。

**FastIoIsQuestionable**  
保留供系统使用。

**SpareC**  
保留供系统使用。

**LockInformation**  
保留供系统使用。

**LastReturnedLockInfo**  
保留供系统使用。

**LastReturnedLock**  
保留供系统使用。

**LockRequestsInProgress**  
保留供系统使用。

<a name="remarks"></a>备注
-------

文件系统旧筛选器驱动程序和微筛选器可以使用不同的例程创建和使用文件\_锁对象，以及针对读/写访问权限的文件。

-   若要分配一个文件\_锁对象，请调用[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)或[ **FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)。

-   若要初始化的未初始化的文件\_锁对象，请调用[ **FsRtlInitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff546122)或[ **FltInitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff543273). 请注意，文件\_从返回锁[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)或[ **FltAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff541743)已经初始化。

-   若要取消初始化文件\_锁对象，请调用[ **FsRtlUninitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547313)或[ **FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)。

-   若要释放文件\_分配的锁对象[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)例程，调用[ **FsRtlFreeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff546011). 若要释放文件\_分配的锁对象[ **FltAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff541743)例程，调用[ **FltFreeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff542969).

一个文件后\_锁已初始化，例程如[ **FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)， [ **FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)，并[ **FsRtlFastCheckLockForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff545918)可用于确定其他线程是否可以访问该文件。

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
<td align="left">Ntifs.h （包括 FltKernel.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

**FltInitializeFileLock**
[**FsRtlAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff545640)

[**FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)

[**FsRtlCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545760)

[**FsRtlFastCheckLockForRead**](https://msdn.microsoft.com/library/windows/hardware/ff545918)

[**FsRtlFastCheckLockForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff545928)

[**FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)

[**FsRtlUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547313)

 

 






