---
title: FLT_PARAMETERS for IRP_MJ_QUERY_OPEN union
description: 当操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段为 IRP_MJ_QUERY_OPEN 时，使用以下联合组件。
ms.assetid: 5B78E1D8-F724-404D-8750-3D52BB9B4910
keywords:
- FLT_PARAMETERS for IRP_MJ_QUERY_OPEN union 可安装的文件系统驱动程序
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
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d05c3efd152226ba6158ffa4318dc5a336e41e0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841362"
---
# <a name="flt_parameters-for-irp_mj_query_open-union"></a>FLT\_IRP_MJ_QUERY_OPEN 联合的参数


当[**FLT\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作**的**块结构为 IRP_MJ_QUERY_OPEN 时，将使用以下联合组件。

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
* 指向调用方分配的缓冲区的指针，例程在该缓冲区中写入有关文件对象的请求信息。 *FileInformationClass*成员指定调用方请求的信息类型。 

**长度**
*  **FileInformation**指向的缓冲区的大小（以字节为单位）。

**FileInformationClass**
* 在 FileInformation 指向的缓冲区中指定要返回的有关文件的信息的类型。 设备和中间驱动程序可以指定以下任何[**FILE_INFORMATION_CLASS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)值。 其他值会导致调用失败，且不应传递给 PreQueryOpen/PostQueryOpen 调用。 

| FILE_INFORMATION_CLASS 值 | 返回的信息的类型 |
| --- | --- |
| FileStatInformation | [**FILE_STAT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)结构。 此结构包含访问掩码。 有关访问掩码的详细信息，请参阅[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)。 
| FileStatLxInformation | [**FILE_STAT_LX_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_lx_information)结构。 此结构包含访问掩码。 有关访问掩码的详细信息，请参阅[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)。 
| FileCaseSensitiveInformation | [FILE_CASE_SENSITIVE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)结构。 |

## <a name="remarks"></a>备注


IRP_MJ_QUERY_OPEN 操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构所表示的**QueryOpen**操作的参数。 它包含在 FLT\_IO\_参数\_块结构。

IRP_MJ_QUERY_OPEN 是一个文件系统（FSFilter）回调操作。

有关 FSFilter 回调操作的详细信息，请参阅[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

## <a name="requirements"></a>要求


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>适用于 windows 10 版本1703及更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
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

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
