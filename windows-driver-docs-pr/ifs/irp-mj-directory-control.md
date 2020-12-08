---
title: 'IRP_MJ_DIRECTORY_CONTROL (IFS) '
description: IRP_MJ_DIRECTORY_CONTROL
keywords:
- IRP_MJ_DIRECTORY_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_DIRECTORY_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bcccfbf8d77413c82f0ffd97529d35b7bd483cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792259"
---
# <a name="irp_mj_directory_control-ifs"></a>IRP_MJ_DIRECTORY_CONTROL (IFS) 

## <a name="when-sent"></a>发送时间

IRP_MJ_DIRECTORY_CONTROL 请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，可以在用户模式应用程序调用 Microsoft Win32 函数（如 **ReadDirectoryChangesW** 或 **FindNextVolumeMountPoint** ）或内核模式组件调用 [**ZwQueryDirectoryFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwquerydirectoryfile)时发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

文件系统驱动程序应检查次要函数代码以确定请求的目录控件操作。 下面是有效的次要函数代码：

| 术语 | 描述 |
| ---- | ----------- |
| IRP_MN_NOTIFY_CHANGE_DIRECTORY | 指示请求通知对目录所做的更改。 通常，文件系统驱动程序将 IRP 保存在专用队列中，而不是立即满足此请求。 当目录发生更改时，文件系统驱动程序将执行通知，并取消排队并完成 IRP。 |
| IRP_MN_QUERY_DIRECTORY | 指示目录查询请求。 可以查询的信息的类型与文件系统相关，但通常包括以下内容： FileBothDirectoryInformation、FileDirectoryInformation、FileFullDirectoryInformation、FileIdBothDirectoryInformation、FileIdFullDirectoryInformation、FileNamesInformation、FileObjectIdInformation、FileReparsePointInformation |

> [!NOTE]
> FileQuotaInformation 信息类已过时。 应改为使用 [**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md) 。

执行请求的操作后，文件系统驱动程序应完成 IRP。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序

筛选器驱动程序必须将此 IRP 传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数

文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理目录控制请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

*DeviceObject*  
指向目标设备对象的指针。

*Irp->IoStatus*  
指向 [**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

*Irp->UserBuffer*  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。

*IrpSp->FileObject*  
指向与 *DeviceObject* 关联的文件对象的指针。

*>IrpSp FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是 FILE_OBJECT 的结构。 FILE_OBJECT 结构的 **RelatedFileObject** 字段在处理 IRP_MJ_DIRECTORY_CONTROL 期间无效，不应使用。

*IrpSp->标志*  
可以为 IRP_MN_QUERY_DIRECTORY 设置以下标志。

| 标志 | 含义 |
| ---- | ------- |
| SL_INDEX_SPECIFIED | 从目录中的条目开始扫描，该目录中的索引由 *>IrpSp 指定。 QueryDirectory. FileIndex*。 |
| SL_RESTART_SCAN | 从目录中的第一个条目开始扫描。 如果未设置此标志，则从上一个 IRP_MN_QUERY_DIRECTORY 请求恢复扫描。 |
| SL_RETURN_SINGLE_ENTRY | 仅返回找到的第一个条目。 |
| SL_RETURN_ON_DISK_ENTRIES_ONLY | 指示执行目录虚拟化或实时扩展的任何筛选器，只需将请求传递到文件系统并返回当前位于磁盘上的项。 |

可以为 IRP_MN_NOTIFY_CHANGE_DIRECTORY 设置以下标志：

| 标志 | 含义 |
| ---- | ------- |
| SL_WATCH_TREE | 如果还应监视此目录的所有子目录，则设置为 **TRUE** 。 如果仅要监视目录本身，则设置为 **FALSE** 。

*IrpSp->MajorFunction*  
指定 IRP_MJ_DIRECTORY_CONTROL。

*IrpSp->MinorFunction*  
下列情况之一：

- IRP_MN_NOTIFY_CHANGE_DIRECTORY
- IRP_MN_QUERY_DIRECTORY

*IrpSp->参数. NotifyDirectory. CompletionFilter*  
有关详细信息，请参阅 [**FsRtlNotifyFullChangeDirectory**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)的 *CompletionFilter* 参数说明。

*IrpSp->参数. NotifyDirectory. 长度*  
Irp 所指向的缓冲区的长度（以字节为单位） *>UserBuffer*。

*IrpSp->参数. QueryDirectory. FileIndex*  
要开始目录扫描的文件的索引。 如果未设置 SL_INDEX_SPECIFIED 标志，则忽略。 不能在任何 Win32 函数或内核模式支持例程中指定此参数。 目前，它仅由 NT 虚拟 DOS 计算机使用 (NTVDM) ，后者仅存在于基于32位 NT 的平台上。 请注意，文件索引对于文件系统是不确定的，例如 NTFS，在这种情况下，父目录中文件的位置不是固定的，可以随时更改以维护排序顺序。

*IrpSp->参数. QueryDirectory. FileInformationClass*  
指定下面描述的值之一。

| “值” | 含义 |
| ----- | ------- |
| **FileBothDirectoryInformation** | 为每个文件返回 [**FILE_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information) 结构。 |
| **FileDirectoryInformation** | 为每个文件返回 [**FILE_DIRECTORY_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information) 结构。 |
| **FileFullDirectoryInformation** | 为每个文件返回 [**FILE_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)"结构。 |
| **FileIdBothDirectoryInformation** | 为每个文件返回 [**FILE_ID_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information) 结构。 |
| **FileIdFullDirectoryInformation** | 为每个文件返回 [**FILE_ID_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information) 结构。 |
| **FileNamesInformation** | 为每个文件返回 [**FILE_NAMES_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information) 结构。 |
| **FileObjectIdInformation** | 为每个文件返回 [**FILE_OBJECTID_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information) 结构。 |
| **FileQuotaInformation** | 已过时。 改用 [IRP_MJ_QUERY_QUOTA](irp-mj-query-quota.md) 。 |
| **FileReparsePointInformation** | 返回目录的单个 [**FILE_REPARSE_POINT_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information) 结构。 |

*IrpSp->参数. QueryDirectory*  
指定目录中的文件的可选名称。

*IrpSp->参数. QueryDirectory. 长度*  
Irp 所指向的缓冲区的长度（以字节为单位） *>UserBuffer*。

## <a name="see-also"></a>请参阅

[**FILE_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**FILE_DIRECTORY_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**FILE_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**FILE_ID_BOTH_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**FILE_ID_FULL_DIR_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**FILE_NAMES_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**FILE_OBJECTID_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**FILE_REPARSE_POINT_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwquerydirectoryfile)
