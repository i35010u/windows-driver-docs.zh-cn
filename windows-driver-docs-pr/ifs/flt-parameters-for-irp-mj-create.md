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
ms.openlocfilehash: d54dd95ae168e5b6245df0d63d2759e98d9614aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577181"
---
# <a name="fltparameters-for-irpmjcreate-union"></a>FLT\_IRP 的参数\_MJ\_创建联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作[ **IRP\_MJ\_创建**](irp-mj-create.md)。

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

指向[**访问权限\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff538840)结构，其中包含对象的使用者上下文，授予其访问权限类型，以及剩余所需访问类型。

SecurityContext-&gt;DesiredAccess

[**访问\_掩码**](https://msdn.microsoft.com/library/windows/hardware/ff540466)结构，它指定为文件请求的访问权限。 有关详细信息，请参阅*DesiredAccess*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

**选项**  
指定要创建或打开该文件，以及该文件已存在时要采取的操作时应用的选项的标志的位掩码。 此成员的较低的 24 位对应于*CreateOptions*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。 高的 8 位对应于*CreateDisposition*参数**FltCreateFile**。

**FileAttributes**  
位屏蔽的属性创建或打开文件时应用。 有关详细信息，请参阅*FileAttributes*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

**ShareAccess**  
为文件请求的共享访问权限的位掩码。 如果此参数为零，正在请求独占访问权限。 有关详细信息，请参阅*ShareAccess*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

**EaLength**  
缓冲区的长度，以字节为单位，该**EaBuffer**成员指向。 有关详细信息，请参阅*EaLength*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

**EaBuffer**  
指向调用方提供，指针[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-包含要应用于的扩展的属性 (EA) 信息的结构化的缓冲区该文件。 有关详细信息，请参阅*EaBuffer*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

**AllocationSize**  
（可选） 指定的初始分配大小，以字节为单位的文件。 一个非零值无任何效果，除非创建文件时，覆盖，还是所取代。 有关详细信息，请参阅*AllocationSize*参数[ **FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_创建**](irp-mj-create.md)操作表示回调数据 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

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


[**ACCESS\_MASK**](https://msdn.microsoft.com/library/windows/hardware/ff540466)

[**ACCESS\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff538840)

[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 






