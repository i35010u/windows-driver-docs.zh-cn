---
title: FLT_PARAMETERS for IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ 时，将使用以下联合组件，\_快速\_IO\_检查\_（如果可能）。
ms.assetid: 1de62b03-4073-40d6-9094-609431e19e5b
keywords:
- FLT_PARAMETERS for IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE union 可安装的文件系统驱动程序
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
ms.openlocfilehash: f3200d6f0e6e038e030a14a1b61ad3b4727d93a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841383"
---
# <a name="flt_parameters-for-irp_mj_fast_io_check_if_possible-union"></a>FLT\_IRP\_MJ\_快速\_IO 的参数\_检查\_是否可行


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)**结构的操作**为 IRP\_MJ 时，使用以下联合组件，\_快速\_IO\_检查\_可以.

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
指定此操作是否要检查是否有读取或写入操作。 对于读取操作，它设置为**TRUE** ，对于写入操作则设置为**FALSE** 。

<a name="remarks"></a>备注
-------

IRP\_MJ 的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构\_快速\_IO\_检查\_如果\_可能的操作包含回调表示的**FastIoCheckIfPossible**操作的参数数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_快速\_IO\_检查\_是否可能是快速的 i/o 操作。

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


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlAreThereCurrentFileLocks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlaretherecurrentfilelocks)

[**FsRtlCopyRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopyread)

[**FsRtlCopyWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopywrite)

 

 






