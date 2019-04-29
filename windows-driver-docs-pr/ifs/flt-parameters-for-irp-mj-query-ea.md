---
title: FLT_PARAMETERS IRP_MJ_QUERY_EA 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_查询\_EA。
ms.assetid: 858e8c72-33ae-441c-ada9-86c5df0e4f59
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_EA 联合可安装文件系统驱动程序
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
ms.openlocfilehash: c929e8e47829b85c33b8604bd422e28e9b17e70d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363071"
---
# <a name="fltparameters-for-irpmjqueryea-union"></a>FLT\_IRP 的参数\_MJ\_查询\_EA 联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_查询\_EA**](irp-mj-query-ea.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                    Length;
    PVOID                    EaList;
    ULONG                    EaListLength;
    ULONG  POINTER_ALIGNMENT EaIndex;
    PVOID                    EaBuffer;
    PMDL                     MdlAddress;
  } QueryEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**QueryEa**  
结构，它包含以下成员。

**长度**  
缓冲区的长度，以字节为单位，该**EaBuffer**指向。

**EaList**  
指向调用方提供，将文件\_获取\_EA\_指定要查询的扩展的属性的信息结构的输入的缓冲区。

**EaListLength**  
缓冲区的长度，以字节为单位，该**EaList**指向。

**EaIndex**  
在其开始扫描的扩展属性列表项的索引。 如果忽略此参数 SL\_索引\_FLT 中未设置指定标志\_IO\_参数\_操作的块结构或者如果**EaList**指向非空的列表。

**EaBuffer**  
指向调用方提供，指针[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)的结构化的输出缓冲区返回扩展的属性值的位置。

**MdlAddress**  
内存描述符列表 (MDL) 描述缓冲区的地址， **EaBuffer**指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_查询\_EA** ](irp-mj-query-ea.md)操作包含回调数据所表示的 IRP 基于查询的扩展的属性的信息操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_查询\_EA 是基于 IRP 的操作。

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


[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IRP\_MJ\_查询\_EA**](irp-mj-query-ea.md)

 

 






