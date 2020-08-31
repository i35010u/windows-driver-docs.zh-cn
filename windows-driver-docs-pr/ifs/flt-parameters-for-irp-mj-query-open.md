---
title: IRP_MJ_QUERY_OPEN 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_QUERY_OPEN 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
ms.assetid: 5B78E1D8-F724-404D-8750-3D52BB9B4910
keywords:
- IRP_MJ_QUERY_OPEN 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
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
ms.openlocfilehash: e8eefaae98b75d17312ceeef1d7b75934011a287
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063620"
---
# <a name="flt_parameters-for-irp_mj_query_open-union"></a>\_IRP_MJ_QUERY_OPEN 联合的 FLT 参数


当 IRP_MJ_QUERY_OPEN 操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时，将使用以下联合组件。

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
* 在 FileInformation 指向的缓冲区中指定要返回的有关文件的信息的类型。 设备和中间驱动程序可以指定以下任何 [**FILE_INFORMATION_CLASS**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class) 值。 其他值会导致调用失败，且不应传递给 PreQueryOpen/PostQueryOpen 调用。 

| FILE_INFORMATION_CLASS 值 | 返回的信息的类型 |
| --- | --- |
| FileStatInformation | [**FILE_STAT_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)结构。 此结构包含访问掩码。 有关访问掩码的详细信息，请参阅 [ACCESS_MASK](../kernel/access-mask.md)。 
| FileStatLxInformation | [**FILE_STAT_LX_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_lx_information)结构。 此结构包含访问掩码。 有关访问掩码的详细信息，请参阅 [ACCESS_MASK](../kernel/access-mask.md)。 
| FileCaseSensitiveInformation | [FILE_CASE_SENSITIVE_INFORMATION](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)结构。 |

## <a name="remarks"></a>备注


IRP_MJ_QUERY_OPEN 操作的[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构的回调数据所表示的**QueryOpen**操作的参数。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP_MJ_QUERY_OPEN 是 (FSFilter) 回调操作的文件系统。

有关 FSFilter 回调操作的详细信息，请参阅 [**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

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
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)