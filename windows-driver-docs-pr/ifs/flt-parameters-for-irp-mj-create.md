---
title: FLT_PARAMETERS for IRP_MJ_CREATE union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_CREATE 时，使用以下联合组件。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- FLT_PARAMETERS for IRP_MJ_CREATE union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 278dab8a1626c3f8c40d5795679a02de8cc36f53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841389"
---
# <a name="flt_parameters-for-irp_mj_create-union"></a>用于 IRP\_MJ\_CREATE union 的 FLT\_参数


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的操作为[**IRP\_MJ\_CREATE**](irp-mj-create.md)**时，使用**以下联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT FileAttributes;
    USHORT                   ShareAccess;
    USHORT POINTER_ALIGNMENT EaLength;
    PVOID                    EaBuffer;
    LARGE_INTEGER            AllocationSize;
  } Create;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**创建**  
包含以下成员的结构。

**SecurityContext**  
SecurityContext-&gt;AccessState

指向[**访问\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

SecurityContext-&gt;DesiredAccess

[**访问\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)结构，用于指定为文件请求的访问权限。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*DesiredAccess*参数。

**选项**  
标志的位掩码，用于指定创建或打开该文件时要应用的选项，以及在文件已存在时要执行的操作。 此成员的低24位对应于[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*CreateOptions*参数。 高8位对应于**FltCreateFile**的*CreateDisposition*参数。

**FileAttributes**  
创建或打开文件时要应用的属性的位掩码。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*FileAttributes*参数。

**ShareAccess**  
为文件请求的共享访问权限位掩码。 如果此参数为零，则请求独占访问。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*ShareAccess*参数。

**EaLength**  
**EaBuffer**成员指向的缓冲区的长度（以字节为单位）。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*EaLength*参数。

**EaBuffer**  
指向调用方提供的、[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构缓冲区的指针，该缓冲区包含要应用于文件的扩展属性（EA）信息。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*EaBuffer*参数。

**AllocationSize**  
（可选）指定文件的初始分配大小（以字节为单位）。 如果创建、覆盖或取代了文件，则非零值将不起作用。 有关详细信息，请参阅[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的*AllocationSize*参数。

<a name="remarks"></a>备注
-------

用于[**IRP\_MJ\_创建**](irp-mj-create.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构，由回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构表示。 它包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

IRP\_MJ\_创建是基于 IRP 的操作。

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


[**访问\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**访问\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**IRP\_MJ\_创建**](irp-mj-create.md)

 

 






