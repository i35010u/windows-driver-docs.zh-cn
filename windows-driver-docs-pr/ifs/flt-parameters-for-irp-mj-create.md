---
title: FLT_PARAMETERS IRP_MJ_CREATE 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_创建。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- FLT_PARAMETERS IRP_MJ_CREATE 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 2b1ec07e063f906516e394124acaccc94f390a4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386078"
---
# <a name="fltparameters-for-irpmjcreate-union"></a>FLT\_IRP 的参数\_MJ\_创建联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构操作[ **IRP\_MJ\_创建**](irp-mj-create.md)。

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
结构，它包含以下成员。

**SecurityContext**  
SecurityContext-&gt;AccessState

指向[**访问权限\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)结构，其中包含对象的使用者上下文，授予其访问权限类型，以及剩余所需访问类型。

SecurityContext-&gt;DesiredAccess

[**访问\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)结构，它指定为文件请求的访问权限。 有关详细信息，请参阅*DesiredAccess*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

**选项**  
指定要创建或打开该文件，以及该文件已存在时要采取的操作时应用的选项的标志的位掩码。 此成员的较低的 24 位对应于*CreateOptions*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。 高的 8 位对应于*CreateDisposition*参数**FltCreateFile**。

**FileAttributes**  
位屏蔽的属性创建或打开文件时应用。 有关详细信息，请参阅*FileAttributes*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

**ShareAccess**  
为文件请求的共享访问权限的位掩码。 如果此参数为零，正在请求独占访问权限。 有关详细信息，请参阅*ShareAccess*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

**EaLength**  
缓冲区的长度，以字节为单位，该**EaBuffer**成员指向。 有关详细信息，请参阅*EaLength*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

**EaBuffer**  
指向调用方提供，指针[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)-包含要应用于的扩展的属性 (EA) 信息的结构化的缓冲区该文件。 有关详细信息，请参阅*EaBuffer*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

**AllocationSize**  
（可选） 指定的初始分配大小，以字节为单位的文件。 一个非零值无任何效果，除非创建文件时，覆盖，还是所取代。 有关详细信息，请参阅*AllocationSize*参数[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构[ **IRP\_MJ\_创建**](irp-mj-create.md)操作表示回调数据 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

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
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ACCESS\_MASK**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**ACCESS\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 






