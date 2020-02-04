---
title: IRP_MJ_DIRECTORY_CONTROL
description: IRP\_MJ\_DIRECTORY\_控件
ms.assetid: cb1bed36-bcb5-419b-87ca-6d9107ece6d1
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
ms.openlocfilehash: 0b66cc6167552f49c0ecb8e77f0c893a15a585d6
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977682"
---
# <a name="irp_mj_directory_control"></a>IRP\_MJ\_DIRECTORY\_控件


## <a name="when-sent"></a>发送时间


IRP\_MJ\_目录\_控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，可以在用户模式应用程序调用 Microsoft Win32 函数（如**ReadDirectoryChangesW**或**FindNextVolumeMountPoint** ）或内核模式组件调用[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)时发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应检查次要函数代码以确定请求的目录控件操作。 下面是有效的次要函数代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_NOTIFY_CHANGE_DIRECTORY</p></td>
<td align="left"><p>指示请求通知对目录所做的更改。 通常，文件系统驱动程序将 IRP 保存在专用队列中，而不是立即满足此请求。 当目录发生更改时，文件系统驱动程序将执行通知，并取消排队并完成 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DIRECTORY</p></td>
<td align="left"><p>指示目录查询请求。 可以查询的信息的类型与文件系统相关，但通常包括以下内容：</p>
FileBothDirectoryInformation FileDirectoryInformation FileFullDirectoryInformation FileIdBothDirectoryInformation FileIdFullDirectoryInformation FileNamesInformation FileObjectIdInformation FileReparsePointInformation</td>
</tr>
</tbody>
</table>

 

&gt; \[！请注意 &gt;\] FileQuotaInformation 信息类已过时。 应改为使用[**IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)。

 

执行请求的操作后，文件系统驱动程序应完成 IRP。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序必须将此 IRP 传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理目录控制请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的输出缓冲区的指针，该缓冲区接收有关目录内容的请求信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_目录\_控制期间无效，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;标志*  
可以为 IRP\_MN\_QUERY\_DIRECTORY 设置以下标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>从目录中的条目开始扫描，该目录中的索引由<em>&gt;IrpSp 指定。 QueryDirectory. FileIndex</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>从目录中的第一个条目开始扫描。 如果未设置此标志，则从上一个 IRP_MN_QUERY_DIRECTORY 请求恢复扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>仅返回找到的第一个条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RETURN_ON_DISK_ENTRIES_ONLY</p></td>
<td align="left"><p>指示执行目录虚拟化或实时扩展的任何筛选器，只需将请求传递到文件系统并返回当前位于磁盘上的项。</p></td>
</tr>
</tbody>
</table>

 

可以为 IRP\_MN 设置以下标志，\_通知\_更改\_目录：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_WATCH_TREE</p></td>
<td align="left"><p>如果还应监视此目录的所有子目录，则设置为<strong>TRUE</strong> 。 如果仅要监视目录本身，则设置为<strong>FALSE</strong> 。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_DIRECTORY\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_通知\_更改\_目录
-   IRP\_MN\_查询\_目录

<a href="" id="irpsp--parameters-notifydirectory-completionfilter"></a>*IrpSp-&gt;参数. NotifyDirectory. CompletionFilter*  
有关详细信息，请参阅[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)的*CompletionFilter*参数说明。

<a href="" id="irpsp--parameters-notifydirectory-length"></a>*IrpSp-&gt;参数. NotifyDirectory. 长度*  
Irp 所指向的缓冲区的长度（以字节为单位） *&gt;UserBuffer*。

<a href="" id="irpsp--parameters-querydirectory-fileindex"></a>*IrpSp-&gt;参数. QueryDirectory. FileIndex*  
要开始目录扫描的文件的索引。 如果未设置\_索引\_指定标志，则忽略。 不能在任何 Win32 函数或内核模式支持例程中指定此参数。 目前它仅由 NT 虚拟 DOS 计算机（NTVDM）使用，后者仅存在于基于32位 NT 的平台上。 请注意，文件索引对于文件系统是不确定的，例如 NTFS，在这种情况下，父目录中文件的位置不是固定的，可以随时更改以维护排序顺序。

<a href="" id="irpsp--parameters-querydirectory-fileinformationclass"></a>*IrpSp-&gt;参数. QueryDirectory. FileInformationClass*  
指定下面描述的值之一。

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
<td align="left"><p><strong>FileBothDirectoryInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)"><strong>FILE_BOTH_DIR_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileDirectoryInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information" data-raw-source="[&lt;strong&gt;FILE_DIRECTORY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)"><strong>FILE_DIRECTORY_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFullDirectoryInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)"><strong>FILE_FULL_DIR_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileIdBothDirectoryInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)"><strong>FILE_ID_BOTH_DIR_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileIdFullDirectoryInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)"><strong>FILE_ID_FULL_DIR_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNamesInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information" data-raw-source="[&lt;strong&gt;FILE_NAMES_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)"><strong>FILE_NAMES_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileObjectIdInformation</strong></p></td>
<td align="left"><p>为每个文件返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information" data-raw-source="[&lt;strong&gt;FILE_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)"><strong>FILE_OBJECTID_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileQuotaInformation</strong></p></td>
<td align="left"><p>此信息类已过时。 应改为使用<a href="irp-mj-query-quota.md" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileReparsePointInformation</strong></p></td>
<td align="left"><p>返回目录的单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information" data-raw-source="[&lt;strong&gt;FILE_REPARSE_POINT_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)"><strong>FILE_REPARSE_POINT_INFORMATION</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-querydirectory-filename"></a>*IrpSp-&gt;参数. QueryDirectory*  
指定目录中的文件的可选名称。

<a href="" id="irpsp--parameters-querydirectory-length"></a>*IrpSp-&gt;参数. QueryDirectory. 长度*  
Irp 所指向的缓冲区的长度（以字节为单位） *&gt;UserBuffer*。

## <a name="see-also"></a>另请参阅


[**文件\_\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**文件\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**文件\_完整\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**文件\_ID\_\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**文件\_ID\_完整\_目录\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**文件\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**文件\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**文件\_重新分析\_点\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_QUERY\_配额**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






