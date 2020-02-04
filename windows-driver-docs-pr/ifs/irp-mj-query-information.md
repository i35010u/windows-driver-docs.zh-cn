---
title: IRP_MJ_QUERY_INFORMATION
description: IRP\_MJ\_QUERY\_INFORMATION
ms.assetid: d25bb277-e14c-4cd8-862a-46b4687bf539
keywords:
- IRP_MJ_QUERY_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 010131afbfb16e8bc325417cfacbe7ee0d7158e7
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977672"
---
# <a name="irp_mj_query_information"></a>IRP\_MJ\_QUERY\_INFORMATION


## <a name="when-sent"></a>发送时间


IRP\_MJ\_查询\_信息请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如**GetFileInformationByHandle** ）或内核模式组件已调用[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是否表示用户打开了文件或目录。 如果是这样，则驱动程序应处理查询并完成 IRP。 否则，驱动程序应视需要完成 IRP，而不处理查询。

可以查询的文件和目录信息的类型与文件系统相关，但通常包括：

FileAllInformation FileAlternateNameInformation FileAttributeTagInformation FileBasicInformation FileCompressionInformation FileEaInformation FileInternalInformation FileNameInformation FileNetworkOpenInformation FilePositionInformation FileStandardInformation FileStreamInformation FileHardLinkInformation，尽管 FileAccessInformation、FileAlignmentInformation 和 FileModeInformation 信息类型也可以作为参数传递给[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)，此信息独立于文件系统。 因此， **ZwQueryInformationFile**直接提供此信息，而无需将 IRP\_MJ\_查询\_信息请求发送到文件系统。

有关这些信息类型的详细信息，请参阅下面的链接。 有关所有可能的信息类型的列表，请参阅 ntifs 中的文件\_信息\_类枚举。

## <a name="operation-network-redirector-drivers"></a>操作：网络重定向程序驱动程序


网络重定向程序驱动程序不基于接收 IRP\_MJ\_查询\_信息请求的 FileAllInformation 或[FileNameInformation 的网络](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)重定向程序驱动程序，必须在服务器名称前使用单个前导反斜杠来响应该文件名的完整 "\\服务器\\共享\\文件" 路径。 对于作为通用命名约定（UNC）名称（例如 *\\\\server\\共享\\文件夹\\filename .txt*）或位于映射的驱动器上的文件（例如，\\*filename .txt*）的文件，必须返回此格式的名称信息。

对于网络微重定向程序驱动程序（使用 rdbss 动态链接的驱动程序，或者使用 rdbsslib 静态链接的驱动程序），IRP\_MJ\_查询 FileNameInformation 的\_信息请求由 RDBSS 在内部进行处理，并返回正确的名称信息。 对于网络最小化重定向程序驱动程序，FileAllInformation 的\_IRP\_查询\_信息请求由 RDBSS 为请求的名称信息部分在内部进行处理。 FileAllInformation 请求的其他部分作为单独的请求发送到网络微型重定向程序驱动程序以进行解析。

如果该文件存在短名称，则接收 IRP\_MJ\_QUERY\_信息请求的网络重定向器应以不含任何路径信息的文件的短名称（8.3 字符）进行响应。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理查询文件信息请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
一个指针，指向要返回文件或目录信息的输出缓冲区。 此信息存储在以下结构之一中：

文件\_所有\_信息

文件\_特性\_标记\_信息

文件\_基本\_信息

文件\_压缩\_信息

文件\_EA\_信息

文件\_内部\_信息

文件\_名称\_信息

文件\_网络\_打开\_信息

文件\_位置\_信息

文件\_标准\_信息

文件\_流\_信息

文件\_链接\_信息

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)中的*IoStatusBlock*参数说明。 例程.

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*指向调用方提供的输出缓冲区的可选指针，在 i/o 管理器的 i/o 完成过程中，将通过 i/o 管理器将*Irp&gt;AssociatedIrp*的内容复制到其中。 驱动程序不使用此缓冲区返回请求的任何数据。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_查询\_信息时无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*指定 IRP\_MJ\_查询\_信息。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*IrpSp-&gt;参数. QueryFile. FileInformationClass*要查询的文件信息的类型。 此成员可以是以下值之一。

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
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_ALL_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返回文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)"><strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返回文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_COMPRESSION_INFORMATION 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_EA_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返回文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)"><strong>FILE_INTERNAL_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返回文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)"><strong>FILE_NAME_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>返回文件的单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)"><strong>FILE_NETWORK_OPEN_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>返回文件的单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>返回文件的单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)"><strong>FILE_STANDARD_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>返回文件的单个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)"><strong>FILE_STREAM_INFORMATION</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileHardLinkInformation</strong></p></td>
<td align="left"><p>返回文件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information" data-raw-source="[&lt;strong&gt;FILE_LINKS_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)"><strong>FILE_LINKS_INFORMATION</strong></a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*IrpSp-&gt;参数. QueryFile. 长度*Irp 所指向的缓冲区的长度（以字节为单位） *-&gt;AssociatedIrp. SystemBuffer*。

<a name="remarks"></a>备注
-------

IRP\_MJ\_QUERY\_信息操作始终由 i/o 管理器进行缓冲。 用于返回所请求的文件或目录信息的*Irp&gt;AssociatedIrp SystemBuffer*由 i/o 管理器从非分页池内存中进行分配。 因此，操作系统返回的*Irp&gt;AssociatedIrp SystemBuffer*将始终是在*IrpSp-&gt;参数. QueryFile*中指定的长度的有效地址。

*Irp&gt;AssociatedIrp UserBuffer*由 i/o 管理器在内部使用，不应由文件系统或文件系统筛选器驱动程序使用。

## <a name="see-also"></a>另请参阅


[**文件\_对齐\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_alignment_information)

[**文件\_特性\_标记\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)

[**文件\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**文件\_内部\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)

[**文件\_名称\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)

[**文件\_网络\_打开\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**文件\_位置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**文件\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[**文件\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**文件\_链接\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_集\_信息**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






