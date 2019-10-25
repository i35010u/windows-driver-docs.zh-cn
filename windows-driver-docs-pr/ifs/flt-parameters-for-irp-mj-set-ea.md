---
title: FLT_PARAMETERS for IRP_MJ_SET_EA union
description: 在 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构时使用的联合组件是 IRP\_MJ\_设置\_EA。
ms.assetid: 92136272-b40b-4f03-ab31-15184aaccd16
keywords:
- FLT_PARAMETERS for IRP_MJ_SET_EA union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 10d74577bb3c8fc85be1e2b9903e43801b955248
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841349"
---
# <a name="flt_parameters-for-irp_mj_set_ea-union"></a>用于 IRP\_MJ\_集\_EA union 的 FLT\_参数


在 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构时使用的联合组件是[**IRP\_MJ\_设置\_EA**](irp-mj-set-ea.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG Length;
    PVOID EaBuffer;
    PMDL  MdlAddress;
  } SetEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetEa**  
包含以下成员的结构。

**长度**  
**EaBuffer**指向的缓冲区的长度（以字节为单位）。

**EaBuffer**  
指向调用方提供的、[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输入缓冲区的指针，其中包含要设置的扩展属性（EA）值。

**MdlAddress**  
描述**EaBuffer**指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，并且可以为**NULL**。

<a name="remarks"></a>备注
-------

[**IRP\_MJ\_集\_EA**](irp-mj-set-ea.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的设置扩展属性-操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_集\_EA 是基于 IRP 的操作。

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

[**IRP\_MJ\_集\_EA**](irp-mj-set-ea.md)

 

 






