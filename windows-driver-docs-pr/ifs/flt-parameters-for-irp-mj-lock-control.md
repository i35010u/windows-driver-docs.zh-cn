---
title: FLT_PARAMETERS for IRP_MJ_LOCK_CONTROL union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_LOCK\_控件时，将使用以下联合组件。
ms.assetid: 4dbdb4c8-5908-40e5-b600-225b47118c6d
keywords:
- FLT_PARAMETERS for IRP_MJ_LOCK_CONTROL union 可安装的文件系统驱动程序
- FLT_PARAMETERS 可安装的可安装文件系统驱动程序
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
ms.openlocfilehash: 8ef19e0d0cd69c38e171b80f726153bff36924b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841379"
---
# <a name="flt_parameters-for-irp_mj_lock_control-union"></a>IRP\_MJ\_锁定\_控制联合的 FLT\_参数


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)**结构的操作**为[**IRP\_MJ\_LOCK\_控件**](irp-mj-lock-control.md)时，将使用以下联合组件。

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
指定在无法立即授予锁定时，锁请求是否应失败的布尔值。 如果请求的线程可以进入等待状态，则将此成员设置为**FALSE** ，直到请求被授予，否则**返回 TRUE** 。

**ExclusiveLock**  
指定是否请求排他锁的布尔值。 如果请求排他锁，则将此成员设置为**TRUE** ，如果请求共享锁，则设置为**FALSE** 。

<a name="remarks"></a>备注
-------

[**IRP\_MJ\_锁定\_控制**](irp-mj-lock-control.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构，由回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构表示。 它包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

IRP\_MJ\_锁定\_控件可以是基于 IRP 的 i/o 操作或快速 i/o 操作。

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
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**访问\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**访问\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**IRP\_MJ\_锁定\_控件**](irp-mj-lock-control.md)

[**PFLT\_完全\_锁定\_回调\_数据\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

[**PUNLOCK\_例程**](punlock-routine.md)

 

 






