---
title: FLT_PARAMETERS for IRP_MJ_QUERY_EA union
description: 在 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构时使用的联合组件是 IRP\_MJ\_查询\_EA。
ms.assetid: 858e8c72-33ae-441c-ada9-86c5df0e4f59
keywords:
- FLT_PARAMETERS for IRP_MJ_QUERY_EA union 可安装的文件系统驱动程序
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
ms.openlocfilehash: e5e658237b121537b4b3590d3b0316e0f7a385cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841381"
---
# <a name="flt_parameters-for-irp_mj_query_ea-union"></a>用于 IRP\_MJ\_查询\_EA union 的 FLT\_参数


在 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构时使用的联合组件是[**IRP\_MJ\_查询\_EA**](irp-mj-query-ea.md)。

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
包含以下成员的结构。

**长度**  
**EaBuffer**指向的缓冲区的长度（以字节为单位）。

**EaList**  
指向提供程序、文件\_的指针将获取\_EA\_信息结构化输入缓冲区来指定要查询的扩展属性。

**EaListLength**  
**EaList**指向的缓冲区的长度（以字节为单位）。

**EaIndex**  
开始扫描扩展属性列表的项的索引。 如果未在\_\_FLT 中设置\_索引\_指定的标志，则将忽略此参数\_操作的块结构，或如果**EaList**指向非空列表，则忽略此参数。

**EaBuffer**  
指向调用方提供的、[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输出缓冲区的指针，将在其中返回扩展属性值。

**MdlAddress**  
描述**EaBuffer**指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，并且可以为**NULL**。

<a name="remarks"></a>备注
-------

用于[**irp\_MJ\_查询\_EA**](irp-mj-query-ea.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的基于 IRP 的查询扩展属性-信息操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_QUERY\_EA 是基于 IRP 的操作。

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


[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IRP\_MJ\_QUERY\_EA**](irp-mj-query-ea.md)

 

 






