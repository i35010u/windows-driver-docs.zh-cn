---
title: FLT_PARAMETERS for IRP_MJ_MDL_WRITE_COMPLETE union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_MDL\_写入\_完成时，将使用以下联合组件。
ms.assetid: 7b3806fb-b6ba-44f5-88fa-883c7896f0ad
keywords:
- FLT_PARAMETERS for IRP_MJ_MDL_WRITE_COMPLETE union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 7deb556a14f83a53e370ecb9670f0a9ab8e37644
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841371"
---
# <a name="flt_parameters-for-irp_mj_mdl_write_complete-union"></a>用于 IRP\_MJ\_MDL 的 FLT\_参数\_写入\_完全联合


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)**结构的操作**为 IRP\_MJ\_MDL\_写入\_完成时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER FileOffset;
    PMDL          MdlChain;
  } MdlWriteComplete;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**MdlWriteComplete**  
包含以下成员的结构。

**FileOffset**  
缓存文件中的起始字节。

**MdlChain**  
指向一个变量的指针，该变量接收指向一个或多个内存描述符列表（MDL）链的指针，该指针描述包含要写入缓存文件的数据的页面。

<a name="remarks"></a>备注
-------

IRP\_MJ\_MDL 的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构\_写入\_完整操作包含回调数据表示的快速 i/o **MdlWriteComplete**操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_MDL\_写入\_完成是一种快速的 i/o 操作。

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

 

 






