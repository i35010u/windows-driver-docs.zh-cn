---
title: IRP_MJ_LOCK_CONTROL 联合的 FLT_PARAMETERS
description: 当操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ LOCK \_ CONTROL 时，将使用以下联合组件。
ms.assetid: 4dbdb4c8-5908-40e5-b600-225b47118c6d
keywords:
- IRP_MJ_LOCK_CONTROL 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
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
ms.openlocfilehash: e96d88aed496cda0cb04f3de514897cfa59a9267
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063630"
---
# <a name="flt_parameters-for-irp_mj_lock_control-union"></a>\_IRP \_ MJ \_ 锁定 \_ 控制联合的 FLT 参数


当操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**IRP \_ MJ \_ LOCK \_ CONTROL**](irp-mj-lock-control.md)时，将使用以下联合组件。

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
包含以下成员的结构。

**长度**  
指向一个变量的指针，该变量指定要锁定的范围的长度（以字节为单位）。

**Key**  
要分配给字节范围锁的键值。

**ByteOffset**  
要锁定的范围内的文件中的起始字节偏移量。

**ProcessId**  
指向请求字节范围锁的进程的进程 ID 的不透明指针。

**FailImmediately**  
指定在无法立即授予锁定时，锁请求是否应失败的布尔值。 如果请求的线程可以进入等待状态，则将此成员设置为 **FALSE** ，直到请求被授予，否则 **返回 TRUE** 。

**ExclusiveLock**  
指定是否请求排他锁的布尔值。 如果请求排他锁，则将此成员设置为 **TRUE** ，如果请求共享锁，则设置为 **FALSE** 。

<a name="remarks"></a>备注
-------

由回调数据表示的[**IRP \_ MJ \_ LOCK \_ 控制**](irp-mj-lock-control.md)操作的[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构， ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

IRP \_ MJ \_ 锁定 \_ 控制可以是基于 IRP 的 i/o 操作，也可以是快速 i/o 操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**访问 \_ 掩码**](../kernel/access-mask.md)

[**访问 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltAllocateFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**IRP \_ MJ \_ 锁定 \_ 控制**](irp-mj-lock-control.md)

[**PFLT \_ 完成 \_ 锁定 \_ 回调 \_ 数据 \_ 例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

[**PUNLOCK \_ 例程**](punlock-routine.md)

 

