---
title: FLT_PARAMETERS for IRP_MJ_MDL_READ_COMPLETE union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_MDL\_读取\_完成时，将使用以下联合组件。
ms.assetid: 1add3569-100d-4c9c-9a62-2333b5bad23b
keywords:
- FLT_PARAMETERS for IRP_MJ_MDL_READ_COMPLETE union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 5a539d03d35cdcaa4741519787d95b958e24539f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841376"
---
# <a name="flt_parameters-for-irp_mj_mdl_read_complete-union"></a>用于 IRP\_MJ\_MDL\_参数的 FLT\_读取\_完整联合


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)**结构的操作**为 IRP\_MJ\_MDL\_读取\_完成时，将使用以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PMDL MdlChain;
  } MdlReadComplete;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**MdlReadComplete**  
包含以下成员的结构。

**MdlChain**  
指向一个变量的指针，该变量接收指向一个或多个内存描述符列表（MDL）链的指针，该指针描述包含要从缓存文件中读取的数据的页面。

<a name="remarks"></a>备注
-------

IRP\_MJ\_MDL 的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构\_读取\_完成操作包含回调数据表示的快速 i/o **MdlReadComplete**操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_MDL\_读取\_完成是一种快速的 i/o 操作。

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

 

 






