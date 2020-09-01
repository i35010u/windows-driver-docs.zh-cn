---
title: IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 联合的 FLT_PARAMETERS
description: 当操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ FAST \_ IO \_ 检查（ \_ 如果 \_ 可能）时，将使用以下联合组件。
ms.assetid: 1de62b03-4073-40d6-9094-609431e19e5b
keywords:
- IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 98b0ebf57b986241adfa65f8ac4b16991d54288c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065244"
---
# <a name="flt_parameters-for-irp_mj_fast_io_check_if_possible-union"></a>\_IRP \_ MJ FAST IO 的 FLT 参数 \_ \_ \_ \_ 如果 \_ 可能，请检查


当操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为 IRP \_ MJ \_ FAST \_ IO \_ 检查（ \_ 如果 \_ 可能）时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER             FileOffset;
    ULONG                     Length;
    ULONG POINTER_ALIGNMENT   LockKey;
    BOOLEAN POINTER_ALIGNMENT CheckForReadOperation;
  } FastIoCheckIfPossible;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**FastIoCheckIfPossible**  
包含以下成员的结构。

**FileOffset**  
缓存文件中的起始字节偏移量。

**长度**  
要读取或写入的数据的长度（以字节为单位）。

**LockKey**  
与目标文件的字节范围锁关联的键值。 如果要读取或写入的范围重叠，或者是文件内 nonexclusively 锁定范围的子范围，则此参数必须是该共享锁的键。 共享锁必须由调用线程的父进程持有;否则，将忽略此参数。

**CheckForReadOperation**  
指定此操作是否要检查是否有读取或写入操作。 对于读取操作，它设置为 **TRUE** ，对于写入操作则设置为 **FALSE** 。

<a name="remarks"></a>备注
-------

IRP MJ 快速 IO 检查的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构（ \_ \_ \_ \_ \_ 如果 \_ 可能的操作包含由回调数据表示的 **FastIoCheckIfPossible** 操作的参数) 结构中 ([**FLT \_ 回叫 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ fast \_ IO \_ 检查（ \_ 如果 \_ 可能）是快速 i/o 操作。

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


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlAreThereCurrentFileLocks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlaretherecurrentfilelocks)

[**FsRtlCopyRead**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopyread)

[**FsRtlCopyWrite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopywrite)

 

