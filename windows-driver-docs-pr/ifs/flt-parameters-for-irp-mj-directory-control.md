---
title: IRP_MJ_DIRECTORY_CONTROL 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_DIRECTORY_CONTROL 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时使用的联合组件。
ms.assetid: 3dadd64b-7e93-4c75-808d-2f26edb3ebd7
keywords:
- IRP_MJ_DIRECTORY_CONTROL 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: ffbf54e3bc5719e69df46d9cb97cb92ecf6d8b16
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064426"
---
# <a name="flt_parameters-for-irp_mj_directory_control-union"></a>IRP_MJ_DIRECTORY_CONTROL 联合的 FLT_PARAMETERS

当[**IRP_MJ_DIRECTORY_CONTROL**](irp-mj-directory-control.md)操作的[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时使用的联合组件。

## <a name="syntax"></a>语法

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

## <a name="members"></a>成员

**DirectoryControl**  
包含以下成员的结构。

**QueryDirectory**  
用于 IRP_MN_QUERY_DIRECTORY 操作的联合组件。

**长度**  
**DirectoryBuffer**成员指向的缓冲区的长度（以字节为单位）。

**FileName**  
指向 [**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构的指针，该结构包含指定目录中的文件的名称。

**FileInformationClass**  
指定下面描述的值之一。

| 值 | 含义 |
|-------|---------|
| FileBothDirectoryInformation   | 为每个文件返回 [**FILE_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information) 结构。                      |
| FileDirectoryInformation       | 为每个文件返回 [**FILE_DIRECTORY_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information) 结构。                     |
| FileFullDirectoryInformation   | 为每个文件返回 [**FILE_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information) 结构。                      |
| FileIdBothDirectoryInformation | 为每个文件返回 [**FILE_ID_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information) 结构。               |
| FileIdFullDirectoryInformation | 为每个文件返回 [**FILE_ID_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information) 结构。               |
| FileNamesInformation           | 为每个文件返回 [**FILE_NAMES_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information) 结构。                             |
| FileObjectIdInformation        | 为每个文件返回 [**FILE_OBJECTID_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information) 结构。                       |
| FileReparsePointInformation    | 返回目录的单个 [**FILE_REPARSE_POINT_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information) 结构。 |

**FileIndex**  
目录扫描开始处的文件的索引。 如果未设置 SL_INDEX_SPECIFIED 标志，则忽略。 不能在任何 Win32 函数或内核模式支持例程中指定此参数。 目前，它仅由 NT 虚拟 DOS 计算机使用 (NTVDM) ，后者仅存在于基于32位 NT 的操作系统上。 请注意，文件索引对于文件系统是不确定的，例如 NTFS，在这种情况下，父目录中文件的位置不是固定的，可以随时更改以维护排序顺序。

**DirectoryBuffer**  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。 此成员是可选的，如果在 **QueryDirectory. MdlAddress**中提供 MDL，则可以为 NULL。 请参阅 " **备注**"。

**MdlAddress**  
 (MDL 的内存描述符列表的地址) 描述 **DirectoryBuffer** 成员指向的缓冲区。 此成员是可选的，如果**QueryDirectory**中提供了缓冲区，则可以为**NULL** 。 请参阅 " **备注**"。

**NotifyDirectory**  
用于 IRP_MN_NOTIFY_CHANGE_DIRECTORY 操作的联合组件。

**长度**  
**DirectoryBuffer**成员指向的缓冲区的长度（以字节为单位）。

**CompletionFilter**  
标志的位掩码，用于指定应在通知列表中完成 Irp 的文件或目录的更改类型。 下面描述了可能的标志值。

| Flag | 含义  |
|------|----------|
| FILE_NOTIFY_CHANGE_FILE_NAME    | 已在此目录中添加、删除或重命名文件。                  |
| FILE_NOTIFY_CHANGE_DIR_NAME     | 已创建、删除或重命名了子目录。                          |
| FILE_NOTIFY_CHANGE_NAME          | 此目录的名称已更改。                                             |
| FILE_NOTIFY_CHANGE_ATTRIBUTES    | 此文件的属性的值（例如 "上次访问时间"）已更改。 |
| FILE_NOTIFY_CHANGE_SIZE          | 此文件的大小已更改。                                                  |
| FILE_NOTIFY_CHANGE_LAST_WRITE   | 此文件的上次修改时间已更改。                                |
| FILE_NOTIFY_CHANGE_LAST_ACCESS  | 此文件的上次访问时间已更改。                                      |
| FILE_NOTIFY_CHANGE_CREATION      | 此文件的创建时间已更改。                                         |
| FILE_NOTIFY_CHANGE_EA            | 已修改此文件的扩展属性。                            |
| FILE_NOTIFY_CHANGE_SECURITY      | 此文件的安全信息已更改。                                  |
| FILE_NOTIFY_CHANGE_STREAM_NAME  | 在此目录中添加、删除或重命名了文件流。           |
| FILE_NOTIFY_CHANGE_STREAM_SIZE  | 此文件流的大小已更改。                                           |
| FILE_NOTIFY_CHANGE_STREAM_WRITE | 此文件流的数据已更改。                                           |

**Spare1**  
当前未使用。

**Spare2**  
当前未使用。

**DirectoryBuffer**  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。 此成员是可选的，如果在 **NotifyDirectory. MdlAddress**中提供 MDL，则可以为 NULL。 请参阅 " **备注**"。

**MdlAddress**  
描述 **NotifyDirectory DirectoryBuffer** 成员指向的缓冲区的 MDL 地址。 此成员是可选的，如果**NotifyDirectory**中提供了缓冲区，则可以为**NULL** 。 请参阅 " **备注**"。

## <a name="remarks"></a>备注

IRP_MJ_DIRECTORY_CONTROL 操作的 [**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构包含一个基于 IRP 的目录控制信息操作的参数，该操作由 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构的回调数据表示。 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

如果同时提供了 **DirectoryBuffer** 和 **MdlAddress** 缓冲区，则建议 minifilters 使用 MDL。 当 **DirectoryBuffer** 指向的内存是在调用进程的上下文中访问的用户模式地址时，或者如果它是内核模式地址，则它是有效的。

如果微筛选器更改 **MdlAddress**的值，则在其后回拨后，筛选器管理器将释放当前存储在 **MDLADDRESS** 中的 MDL，并还原以前的 **MdlAddress**值。

IRP_MJ_DIRECTORY_CONTROL 是基于 IRP 的操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>另请参阅

[**FILE_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**FILE_DIRECTORY_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**FILE_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**FILE_ID_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**FILE_ID_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**FILE_NAMES_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**FILE_OBJECTID_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**FILE_REPARSE_POINT_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltNotifyFilterChangeDirectory**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltnotifyfilterchangedirectory)

[**FsRtlNotifyFilterChangeDirectory**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterchangedirectory)

[**Fsrtlnotifyfilterreportchange 并且**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)

[**FsRtlNotifyFullChangeDirectory**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**FsRtlNotifyFullReportChange**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullreportchange)

[**IRP_MJ_DIRECTORY_CONTROL**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](/previous-versions/ff567047(v=vs.85))