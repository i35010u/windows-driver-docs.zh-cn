---
title: FLT_PARAMETERS IRP_MJ_LOCK_CONTROL 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_锁\_控件。
ms.assetid: 4dbdb4c8-5908-40e5-b600-225b47118c6d
keywords:
- FLT_PARAMETERS IRP_MJ_LOCK_CONTROL 联合可安装文件系统驱动程序
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84304a4abd2e921a06c0e78d7886651d1a45b1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364987"
---
# <a name="fltparameters-for-irpmjlockcontrol-union"></a>FLT\_IRP 的参数\_MJ\_锁\_控件联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作[ **IRP\_MJ\_锁\_控制**](irp-mj-lock-control.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PLARGE_INTEGER          Length;
    ULONG POINTER_ALIGNMENT Key;
    LARGE_INTEGER           ByteOffset;
    PEPROCESS               ProcessId;
    BOOLEAN                 FailImmediately;
    BOOLEAN                 ExclusiveLock;
  } LockControl;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**LockControl**  
结构，它包含以下成员。

**长度**  
为指定的长度以字节为单位的要锁定的范围的变量的指针。

**Key**  
要分配给字节范围锁定的密钥值。

**ByteOffset**  
起始范围被锁定的文件中的字节偏移量。

**ProcessId**  
不透明指针，指向请求的字节范围锁的进程的进程 ID。

**FailImmediately**  
布尔值，该值指定是否锁不能立即授予锁定请求是否应失败。 此成员设置为**FALSE**如果请求的线程可以将置于等待状态，直到授予的请求或**TRUE**如果不能。

**ExclusiveLock**  
布尔值，该值指定是否将请求的排他锁。 此成员设置为 **，则返回 TRUE**如果请求的排他锁或**FALSE**如果请求共享的锁。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_锁定\_控件**](irp-mj-lock-control.md)表示的回调数据操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

IRP\_MJ\_锁\_控件可以是基于 IRP 的 I/O 操作或快速 I/O 操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ACCESS\_MASK**](https://msdn.microsoft.com/library/windows/hardware/ff540466)

[**ACCESS\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff538840)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff542969)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

[**FltProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543427)

[**FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)

[**IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md)

[**PFLT\_COMPLETE\_LOCK\_CALLBACK\_DATA\_ROUTINE**](https://msdn.microsoft.com/library/windows/hardware/ff551073)

[**PUNLOCK\_例程**](punlock-routine.md)

 

 






