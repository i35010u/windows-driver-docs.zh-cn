---
title: FLT_PARAMETERS IRP_MJ_WRITE 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_编写。
ms.assetid: c40d4c9e-2d09-4cd1-9278-5067dad2914f
keywords:
- FLT_PARAMETERS IRP_MJ_WRITE 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 1b0d96392670876e0076ee942404799064e61156
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393034"
---
# <a name="fltparameters-for-irpmjwrite-union"></a>FLT\_IRP 的参数\_MJ\_写入联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作[ **IRP\_MJ\_编写**](irp-mj-write.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG         Length;
    ULONG         Key;
    LARGE_INTEGER ByteOffset;
    PVOID         WriteBuffer;
    PMDL          MdlAddress;
  } Write;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**编写**  
结构，它包含以下成员。

**长度**  
长度 （字节），要写入的数据。

**Key**  
目标文件的字节范围锁与关联的密钥值。

**ByteOffset**  
要写入的数据文件中的起始字节偏移量。

**WriteBuffer**  
指向包含要写入到文件的数据的缓冲区的指针。

**MdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， **WriteBuffer**成员指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_写入操作包含回调数据 (所表示的写入操作的参数[**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_写入可以是基于 IRP 的操作或快速 I/O 操作。

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

[**FltWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff544610)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

[**ZwWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff567121)

 

 






