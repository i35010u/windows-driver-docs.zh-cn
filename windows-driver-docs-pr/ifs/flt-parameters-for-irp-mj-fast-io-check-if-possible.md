---
title: FLT_PARAMETERS IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_快速\_IO\_检查\_如果\_可能。
ms.assetid: 1de62b03-4073-40d6-9094-609431e19e5b
keywords:
- FLT_PARAMETERS IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 92466dda6f9931b436bd4d45c93a20bc985c33e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380351"
---
# <a name="fltparameters-for-irpmjfastiocheckifpossible-union"></a>FLT\_IRP 的参数\_MJ\_快速\_IO\_检查\_如果\_可能联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构，该操作是 IRP\_MJ\_快速\_IO\_检查\_如果\_可能。

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
结构，它包含以下成员。

**FileOffset**  
缓存文件中的起始字节偏移量。

**长度**  
长度 （字节），要读取或写入的数据。

**LockKey**  
目标文件的字节范围锁与关联的密钥值。 如果要读取或写入的范围重叠，或者是该文件中的非独占方式锁定范围的子范围，此参数必须为该共享锁的键。 必须通过调用线程; 的父进程持有共享的锁否则，将忽略此参数。

**CheckForReadOperation**  
指定是否为此操作，检查对于读取或写入操作。 设置为 **，则返回 TRUE**的读操作和**FALSE**写入操作。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构 IRP\_MJ\_快速\_IO\_检查\_如果\_可能的操作包含的参数**FastIoCheckIfPossible**表示的回调数据操作 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_快速\_IO\_检查\_如果\_可能是一个快速的 I/O 操作。

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


[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlAreThereCurrentFileLocks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlaretherecurrentfilelocks)

[**FsRtlCopyRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopyread)

[**FsRtlCopyWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopywrite)

 

 






