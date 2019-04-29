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
ms.openlocfilehash: 168968665c215adcb7a540b12f2564d567d6ffad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365005"
---
# <a name="fltparameters-for-irpmjfastiocheckifpossible-union"></a>FLT\_IRP 的参数\_MJ\_快速\_IO\_检查\_如果\_可能联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构，该操作是 IRP\_MJ\_快速\_IO\_检查\_如果\_可能。

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

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_快速\_IO\_检查\_如果\_可能的操作包含的参数**FastIoCheckIfPossible**表示的回调数据操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

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


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FsRtlAreThereCurrentFileLocks**](https://msdn.microsoft.com/library/windows/hardware/ff545697)

[**FsRtlCopyRead**](https://msdn.microsoft.com/library/windows/hardware/ff545791)

[**FsRtlCopyWrite**](https://msdn.microsoft.com/library/windows/hardware/ff545797)

 

 






