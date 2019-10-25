---
title: FLT_PARAMETERS for IRP_MJ_DIRECTORY_CONTROL union
description: 当 FLT\_IO\_参数\_块结构的操作为 IRP\_MJ\_DIRECTORY\_CONTROL 时使用的联合组件。
ms.assetid: 3dadd64b-7e93-4c75-808d-2f26edb3ebd7
keywords:
- FLT_PARAMETERS for IRP_MJ_DIRECTORY_CONTROL union 可安装的文件系统驱动程序
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
ms.openlocfilehash: c2c5c2cae4f514acc62514a50cc27a2551428132
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841385"
---
# <a name="flt_parameters-for-irp_mj_directory_control-union"></a>用于 IRP 的 FLT\_参数\_MJ\_目录\_控制联合


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的操作为[**IRP\_MJ\_DIRECTORY\_CONTROL**](irp-mj-directory-control.md)时**使用的联合**组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      ULONG                   Length;
      PUNICODE_STRING         FileName;
      FILE_INFORMATION_CLASS  FileInformationClass;
      ULONG POINTER_ALIGNMENT FileIndex;
      PVOID                   DirectoryBuffer;
      PMDL                    MdlAddress;
    } QueryDirectory;
    struct {
      ULONG                   Length;
      ULONG POINTER_ALIGNMENT CompletionFilter;
      ULONG                   Spare1;
      ULONG POINTER_ALIGNMENT Spare2;
      PVOID                   DirectoryBuffer;
      PMDL                    MdlAddress;
    } NotifyDirectory;
  } DirectoryControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**DirectoryControl**  
包含以下成员的结构。

**QueryDirectory**  
用于 IRP\_MN\_QUERY\_DIRECTORY 操作的联合组件。

**长度**  
**DirectoryBuffer**成员指向的缓冲区的长度（以字节为单位）。

**名字**  
指向[**UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)结构的指针，该字符串结构包含指定目录中的文件的名称。

**FileInformationClass**  
指定下面描述的值之一。

| Value                          | 含义                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| FileBothDirectoryInformation   | 为每个文件返回[ **\_\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)结构的文件。                      |
| FileDirectoryInformation       | 为每个文件返回[ **\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)结构的文件。                     |
| FileFullDirectoryInformation   | 为每个文件返回[ **\_完整\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)结构的文件。                      |
| FileIdBothDirectoryInformation | 返回[ **\_ID 的文件\_每个文件\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)结构。               |
| FileIdFullDirectoryInformation | 为每个文件返回[ **\_ID\_完整\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)结构的文件。               |
| FileNamesInformation           | 为每个文件返回[ **\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)结构的文件。                             |
| FileObjectIdInformation        | 为每个文件返回[ **\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)结构的文件。                       |
| FileReparsePointInformation    | 返回\_重新[**分析\_点\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)目录的单个文件。 |

 

**FileIndex**  
目录扫描开始处的文件的索引。 如果未设置\_索引\_指定标志，则忽略。 不能在任何 Win32 函数或内核模式支持例程中指定此参数。 目前它仅由 NT 虚拟 DOS 计算机（NTVDM）使用，后者仅存在于基于32位 NT 的操作系统上。 请注意，文件索引对于文件系统是不确定的，例如 NTFS，在这种情况下，父目录中文件的位置不是固定的，可以随时更改以维护排序顺序。

**DirectoryBuffer**  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。

**MdlAddress**  
描述**QueryDirectory DirectoryBuffer**成员指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，并且可以为**NULL**。

**NotifyDirectory**  
用于 IRP\_MN 的联合组件\_通知\_更改\_目录操作。

**长度**  
**DirectoryBuffer**成员指向的缓冲区的长度（以字节为单位）。

**CompletionFilter**  
标志的位掩码，用于指定应在通知列表中完成 Irp 的文件或目录的更改类型。 下面描述了可能的标志值。

| 旗帜                                | 含义                                                                        |
|-------------------------------------|--------------------------------------------------------------------------------|
| 文件\_通知\_更改\_文件\_名称    | 已在此目录中添加、删除或重命名文件。                  |
| 文件\_通知\_更改\_目录\_名称     | 已创建、删除或重命名了子目录。                          |
| 文件\_通知\_更改\_名称          | 此目录的名称已更改。                                             |
| 文件\_通知\_更改\_特性    | 此文件的属性的值（例如 "上次访问时间"）已更改。 |
| 文件\_通知\_更改\_大小          | 此文件的大小已更改。                                                  |
| 文件\_通知\_更改\_最后\_写入   | 此文件的上次修改时间已更改。                                |
| 文件\_通知\_更改\_上次\_访问  | 此文件的上次访问时间已更改。                                      |
| 文件\_通知\_创建\_更改      | 此文件的创建时间已更改。                                         |
| 文件\_通知\_更改\_EA            | 已修改此文件的扩展属性。                            |
| 文件\_通知\_更改\_安全性      | 此文件的安全信息已更改。                                  |
| 文件\_通知\_更改\_流\_名称  | 在此目录中添加、删除或重命名了文件流。           |
| 文件\_通知\_更改\_流\_大小  | 此文件流的大小已更改。                                           |
| 文件\_通知\_更改\_流\_写入 | 此文件流的数据已更改。                                           |

 

**Spare1**  
当前未使用。

**Spare2**  
当前未使用。

**DirectoryBuffer**  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。

**MdlAddress**  
描述**NotifyDirectory DirectoryBuffer**成员指向的缓冲区的 MDL 地址。 此成员是可选的，并且可以为**NULL**。

<a name="remarks"></a>备注
-------

IRP\_MJ\_目录\_控制操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的基于 IRP 的目录控制信息操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_DIRECTORY\_控件是基于 IRP 的操作。

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


[**文件\_\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**文件\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**文件\_完整\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**文件\_ID\_\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**文件\_ID\_完整\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**文件\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**文件\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**文件\_重新分析\_点\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltnotifyfilterchangedirectory)

[**FsRtlNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterchangedirectory)

[**Fsrtlnotifyfilterreportchange 并且**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**FsRtlNotifyFullReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullreportchange)

[**IRP\_MJ\_DIRECTORY\_控件**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






