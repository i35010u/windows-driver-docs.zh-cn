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
ms.openlocfilehash: dfeba975abf3b203a0fdcd590c9cf82578a3459e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384834"
---
# <a name="irpmjdirectorycontrol"></a>IRP\_MJ\_DIRECTORY\_控件


## <a name="when-sent"></a>发送时间


IRP\_MJ\_DIRECTORY\_控制请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**ReadDirectoryChangesW**或**FindNextVolumeMountPoint**或当调用内核模式组件[ **ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应检查次要函数代码，以确定请求的目录管理操作。 以下是有效的次要函数代码：

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
<td align="left"><p>指示对目录的更改通知的请求。 通常情况下，而不是立即满足此请求，文件系统驱动程序持有 IRP 的专用队列。 到的目录，发生了更改，文件系统驱动程序执行通知和取消排队并完成 IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DIRECTORY</p></td>
<td align="left"><p>指示目录查询请求。 可以查询的信息类型的文件系统相关，但通常包括以下各项：</p>
FileBothDirectoryInformation FileDirectoryInformation FileFullDirectoryInformation FileIdBothDirectoryInformation FileIdFullDirectoryInformation FileNamesInformation FileObjectIdInformation FileReparsePointInformation</td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\] &gt; FileQuotaInformation 信息类已过时。 [**IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)应改为使用。

 

执行请求的操作，在文件系统驱动程序应完成 IRP。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序必须在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理目录控制请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向接收内容的目录的请求的有关的调用方提供输出缓冲区的指针。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_DIRECTORY\_控件，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  
可以为 IRP 设置以下标志\_MN\_查询\_目录。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>开始在给定其索引的目录中的条目扫描<em>IrpSp-&gt;Parameters.QueryDirectory.FileIndex</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>开始扫描目录中的第一个条目。 如果未设置此标志，继续从上一个 IRP_MN_QUERY_DIRECTORY 请求扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>返回只找到的第一个条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RETURN_ON_DISK_ENTRIES_ONLY</p></td>
<td align="left"><p>指示执行目录虚拟化或在实时扩展，只需将请求传递到文件系统，并返回当前在磁盘上的条目的任何筛选器。</p></td>
</tr>
</tbody>
</table>

 

以下标志可设置为 IRP\_MN\_通知\_更改\_目录：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_WATCH_TREE</p></td>
<td align="left"><p>设置为<strong>，则返回 TRUE</strong>如果此目录的所有子目录也应进行都监视。 设置为<strong>FALSE</strong>如果只是监视其自身的目录。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_DIRECTORY\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_通知\_更改\_目录
-   IRP\_MN\_查询\_目录

<a href="" id="irpsp--parameters-notifydirectory-completionfilter"></a>*IrpSp-&gt;Parameters.NotifyDirectory.CompletionFilter*  
有关详细信息，请参阅的说明*CompletionFilter*参数[ **FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)。

<a href="" id="irpsp--parameters-notifydirectory-length"></a>*IrpSp-&gt;Parameters.NotifyDirectory.Length*  
指向缓冲区的长度以字节为单位*Irp-&gt;UserBuffer*。

<a href="" id="irpsp--parameters-querydirectory-fileindex"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileIndex*  
要开始目录扫描文件的索引。 已忽略的如果 SL\_索引\_未设置指定标志。 不能在任何 Win32 函数或内核模式下支持例程中指定此参数。 当前它只能由仅在 32 位基于 NT 的平台存在的 NT 虚拟 DOS 机 (NTVDM) 使用。 请注意，文件索引的文件系统，如 NTFS，在其中的父目录中的文件的位置不固定的可以在任何时维护排序顺序更改未定义。

<a href="" id="irpsp--parameters-querydirectory-fileinformationclass"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileInformationClass*  
指定其中一个如下所述的值。

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
<td align="left"><p><strong>FileBothDirectoryInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)"> <strong>FILE_BOTH_DIR_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileDirectoryInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information" data-raw-source="[&lt;strong&gt;FILE_DIRECTORY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)"> <strong>FILE_DIRECTORY_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFullDirectoryInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)"> <strong>FILE_FULL_DIR_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileIdBothDirectoryInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)"> <strong>FILE_ID_BOTH_DIR_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileIdFullDirectoryInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)"> <strong>FILE_ID_FULL_DIR_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNamesInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information" data-raw-source="[&lt;strong&gt;FILE_NAMES_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)"> <strong>FILE_NAMES_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileObjectIdInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information" data-raw-source="[&lt;strong&gt;FILE_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)"> <strong>FILE_OBJECTID_INFORMATION</strong> </a>为每个文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileQuotaInformation</strong></p></td>
<td align="left"><p>此信息类已过时。 <a href="irp-mj-query-quota.md" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong> </a>应改为使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileReparsePointInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information" data-raw-source="[&lt;strong&gt;FILE_REPARSE_POINT_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)"> <strong>FILE_REPARSE_POINT_INFORMATION</strong> </a>目录结构。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-querydirectory-filename"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileName*  
指定的目录中的文件的可选名称。

<a href="" id="irpsp--parameters-querydirectory-length"></a>*IrpSp-&gt;Parameters.QueryDirectory.Length*  
指向缓冲区的长度以字节为单位*Irp-&gt;UserBuffer*。

## <a name="see-also"></a>请参阅


[**文件\_两者\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)

[**文件\_DIRECTORY\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)

[**文件\_完整\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)

[**文件\_ID\_同时\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)

[**文件\_ID\_完整\_DIR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)

[**文件\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)

[**文件\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)

[**FILE\_REPARSE\_POINT\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






