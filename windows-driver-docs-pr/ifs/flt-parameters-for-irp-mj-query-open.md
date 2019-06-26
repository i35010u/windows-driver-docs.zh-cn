---
title: FLT_PARAMETERS IRP_MJ_QUERY_OPEN 联合
description: 该操作的 FLT_IO_PARAMETER_BLOCK 结构在 MajorFunction 字段 IRP_MJ_QUERY_OPEN 时使用以下联合组件。
ms.assetid: 5B78E1D8-F724-404D-8750-3D52BB9B4910
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_OPEN 联合可安装文件系统驱动程序
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
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0338b7e5191076f178f827c801f68d589e3d171d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365484"
---
# <a name="fltparameters-for-irpmjqueryopen-union"></a>FLT\_IRP_MJ_QUERY_OPEN 联合的参数


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的结构是 IRP_MJ_QUERY_OPEN。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIRP                   Irp;
    PVOID                  FileInformation;
    PULONG                 Length;
    FILE_INFORMATION_CLASS FileInformationClass;
  } QueryOpen;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**Irp**  
* 指向与此操作关联的 IRP 的指针。 

**FileInformation**  
* 指向该例程将文件对象的请求的信息写入到其中的调用方分配的缓冲区的指针。 *FileInformationClass*成员指定的调用方请求的信息类型。 

**长度**
*  大小 （字节） 通过指向的缓冲区**FileInformation**。

**FileInformationClass**
* 指定要返回关于 FileInformation 指向的缓冲区中的文件的信息类型。 设备和中间驱动程序可以指定任何以下[ **FILE_INFORMATION_CLASS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)值。 其他值会导致调用失败，并且不应传递给 PreQueryOpen/PostQueryOpen 调用。 

| FILE_INFORMATION_CLASS 值 | 返回的信息类型 |
| --- | --- |
| FileStatInformation | 一个[ **FILE_STAT_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_information)结构。 此结构包含的访问掩码。 有关访问掩码的详细信息，请参阅[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)。 
| FileStatLxInformation | 一个[ **FILE_STAT_LX_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_lx_information)结构。 此结构包含的访问掩码。 有关访问掩码的详细信息，请参阅[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)。 
| FileCaseSensitiveInformation | 一个[FILE_CASE_SENSITIVE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_information)结构。 |

## <a name="remarks"></a>备注


[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP_MJ_QUERY_OPEN 操作的结构中包含的参数**QueryOpen**表示回调的操作数据 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP_MJ_QUERY_OPEN 是文件系统 (FSFilter) 回调操作。

有关 FSFilter 回调操作的详细信息，请参阅引用条目[ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)。

## <a name="requirements"></a>要求


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 10，版本 1703年和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
