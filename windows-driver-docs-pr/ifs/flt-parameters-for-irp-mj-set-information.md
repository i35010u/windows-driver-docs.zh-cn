---
title: FLT_PARAMETERS for IRP_MJ_SET_INFORMATION union
description: 在 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构时使用的联合组件是 IRP\_MJ\_设置\_信息。
ms.assetid: 860973bf-a98d-4495-9d6c-093ee985f360
keywords:
- FLT_PARAMETERS for IRP_MJ_SET_INFORMATION union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 78d44630a1fbb2741691dfb515d01122a4313044
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841350"
---
# <a name="flt_parameters-for-irp_mj_set_information-union"></a>用于 IRP\_MJ\_集\_信息联合的 FLT\_参数


在 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构时使用的联合组件是[**IRP\_MJ\_设置\_信息**](irp-mj-set-information.md)。

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
要为文件设置的信息类型。 下列情况之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)"><strong>FILE_ALLOCATION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)"><strong>FILE_DISPOSITION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)"><strong>FILE_END_OF_FILE_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)"><strong>FILE_LINK_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)"><strong>FILE_RENAME_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>设置文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)"><strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**ParentOfTarget**  
用于重命名或链接操作。 如果**InfoBuffer&gt;FileName**包含完全限定的文件名，或者**InfoBuffer-&gt;RootDirectory**非**NULL**，则此成员是文件的父目录的文件对象指针，该文件是运作. 否则为**NULL**。

（*未命名的结构*）  
包含以下成员的结构。

**ReplaceIfExists**  
用于重命名或链接操作。 如果设置为**TRUE** ，则指定已存在的同名文件将替换为给定的文件。 如果重命名或链接操作如果已存在具有给定名称的文件，则设置为**FALSE** 。

**AdvanceOnly**  
文件结尾操作的标志。 这会确定在**FileInformationClass** == **FileEndOfFileInformation**时，使用**EndOfFile**成员[**文件\_端\_\_文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)结构。 如果**为 TRUE**，则仅当文件增加当前有效数据长度时，才从**EndOfFile**设置新的有效数据长度。 如果**为 FALSE**，则从**EndOfFile**设置新的文件大小。

**ClusterCount**  
保留供系统使用。 不使用。

**DeleteHandle**  
保留供系统使用。 不使用。

**InfoBuffer**  
指向包含要设置的文件信息的输入缓冲区的指针。

<a name="remarks"></a>备注
-------

IRP\_MJ\_集\_信息操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的集信息操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）构造. 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_集\_信息是基于 IRP 的操作。

缓存管理器将**AdvanceOnly**成员设置为**TRUE** ，以通知文件系统将磁盘上的当前有效数据长度提升到**EndOfFile**中的新有效数据长度。 如果**AdvanceOnly**为**FALSE**，则会设置**EndOfFile**成员中的新文件大小，该大小可大于或小于当前文件大小。

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


[**文件\_分配\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**文件\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**文件\_处置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**文件\_结束\_\_文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**文件\_链接\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**文件\_位置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**文件\_重命名\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**文件\_有效的\_数据\_长度\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_集\_信息**](irp-mj-set-information.md)

 

 






