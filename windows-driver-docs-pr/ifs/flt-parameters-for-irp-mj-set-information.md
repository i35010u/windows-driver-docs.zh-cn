---
title: IRP_MJ_SET_INFORMATION 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 IRP \_ MJ \_ 集 \_ 信息时使用的联合组件。
ms.assetid: 860973bf-a98d-4495-9d6c-093ee985f360
keywords:
- IRP_MJ_SET_INFORMATION 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4ee6b1762cd6678155de93789b5b37dde08d548
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106760"
---
# <a name="flt_parameters-for-irp_mj_set_information-union"></a>\_IRP \_ MJ \_ 集 \_ 信息联合的 FLT 参数


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**IRP \_ MJ \_ 集 \_ 信息**](irp-mj-set-information.md)时使用的联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                    Length;
    FILE_INFORMATION_CLASS POINTER_ALIGNMENT FileInformationClass;
    PFILE_OBJECT                             ParentOfTarget;
    union {
      struct {
        BOOLEAN ReplaceIfExists;
        BOOLEAN AdvanceOnly;
      };
      ULONG  ClusterCount;
      HANDLE DeleteHandle;
    };
    PVOID                                    InfoBuffer;
  } SetFileInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetFileInformation**  
包含以下成员的结构。

**长度**  
**InfoBuffer**缓冲区的长度（以字节为单位）。

**FileInformationClass**  
要为文件设置的信息类型。 下列类型作之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)"><strong>FILE_ALLOCATION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)"><strong>FILE_DISPOSITION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)"><strong>FILE_END_OF_FILE_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)"><strong>FILE_LINK_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)"><strong>FILE_RENAME_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>为文件设置 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)"><strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**ParentOfTarget**  
用于重命名或链接操作。 如果 **InfoBuffer 包含 &gt; ** 完全限定的文件名，或者 **InfoBuffer- &gt; RootDirectory** 为非**NULL**，则此成员是作为操作目标的文件的父目录的文件对象指针。 否则为 **NULL**。

 ( *未命名结构* )   
包含以下成员的结构。

**ReplaceIfExists**  
用于重命名或链接操作。 如果设置为 **TRUE** ，则指定已存在的同名文件将替换为给定的文件。 如果重命名或链接操作如果已存在具有给定名称的文件，则设置为 **FALSE** 。

**AdvanceOnly**  
文件结尾操作的标志。 这会确定在**FileInformationClass**FileEndOfFileInformation 时，使用**EndOfFile**成员[**文件的 \_ \_ \_ 文件 \_ 结尾**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)  ==  **FileEndOfFileInformation**。 如果 **为 TRUE**，则仅当文件增加当前有效数据长度时，才从 **EndOfFile** 设置新的有效数据长度。 如果 **为 FALSE**，则从 **EndOfFile**设置新的文件大小。

**ClusterCount**  
预留给系统使用。 请勿使用。

**DeleteHandle**  
预留给系统使用。 请勿使用。

**InfoBuffer**  
指向包含要设置的文件信息的输入缓冲区的指针。

<a name="remarks"></a>备注
-------

IRP MJ 集信息操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构 \_ \_ \_ 包含由回调数据表示的集信息操作的参数) 结构中 ([**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 。 它包含在 FLT \_ IO \_ 参数 \_ 块结构中。

IRP \_ MJ \_ 集 \_ 信息是基于 IRP 的操作。

缓存管理器将 **AdvanceOnly** 成员设置为 **TRUE** ，以通知文件系统将磁盘上的当前有效数据长度提升到 **EndOfFile**中的新有效数据长度。 如果 **AdvanceOnly** 为 **FALSE**，则会设置 **EndOfFile** 成员中的新文件大小，该大小可大于或小于当前文件大小。

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
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件 \_ 分配 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**文件 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**文件 \_ 处置 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**文件 \_ 末尾 \_ 的 \_ 文件 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**文件 \_ 链接 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**文件 \_ 位置 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**文件 \_ 重命名 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**文件 \_ 有效的 \_ 数据 \_ 长度 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP \_ MJ \_ 设置 \_ 信息**](irp-mj-set-information.md)

