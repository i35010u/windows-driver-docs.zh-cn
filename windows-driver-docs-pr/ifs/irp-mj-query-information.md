---
title: IRP_MJ_QUERY_INFORMATION
description: IRP\_MJ\_查询\_信息
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
ms.openlocfilehash: 7de1812876bd03cf21fb598d34d0fd223022c5e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520397"
---
# <a name="irpmjqueryinformation"></a>IRP\_MJ\_查询\_信息


## <a name="when-sent"></a>发送时间


IRP\_MJ\_查询\_由 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序发送的信息请求。 可以将发送此请求，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**GetFileInformationByHandle**或当调用内核模式组件[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定它是否表示打开的文件或目录的用户的文件对象。 如果是这样，该驱动程序应处理该查询，并完成 IRP。 否则，驱动程序应完成根据 IRP，而不会处理该查询。

可以查询的文件和目录信息的类型是文件系统相关，但通常包括以下各项：

FileAllInformation FileAlternateNameInformation FileAttributeTagInformation FileBasicInformation FileCompressionInformation FileEaInformation FileInternalInformation FileNameInformation FileNetworkOpenInformationFilePositionInformation FileStandardInformation FileStreamInformation FileHardLinkInformation 尽管 FileAccessInformation、 FileAlignmentInformation 和 FileModeInformation 信息类型可以也将作为参数传递到[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)，此信息是独立于系统文件。 从而**ZwQueryInformationFile**提供此信息直接，而无需发送 IRP\_MJ\_查询\_到文件系统的信息请求。

有关这些信息类型的详细信息，请参阅下面的另请参阅链接。 有关所有可能的信息类型的列表，请参阅该文件\_信息\_中 ntifs.h 类枚举。

## <a name="operation-network-redirector-drivers"></a>操作：网络重定向程序驱动程序


网络重定向程序驱动程序不基于[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)接收 IRP\_MJ\_查询\_FileAllInformation 或 FileNameInformation，信息请求必须与完整"做出响应\\服务器\\共享\\文件"与单个前导反斜杠之前的服务器名称的文件名称的路径。 此名称的信息的格式必须返回作为通用命名约定 (UNC) 名称访问的文件 (*\\\\服务器\\共享\\文件夹\\文件名.txt*，例如) 或位于映射的驱动器上的文件 (*x:\\文件夹\\文件名.txt*，例如)。

有关网络微型重定向程序驱动程序 （驱动程序的动态链接到 rdbss.sys 或以静态方式链接与 rdbsslib.lib），IRP\_MJ\_查询\_在内部处理 FileNameInformation 的信息请求由 RDBSS 和正确的名称返回信息。 对于网络微型重定向程序驱动程序，IRP\_MJ\_查询\_FileAllInformation 的信息请求通过名称信息请求的一部分的 RDBSS 在内部处理。 FileAllInformation 请求的其他部分发送为单独的请求到网络的最小重定向程序驱动程序来解决。

网络重定向程序接收 IRP\_MJ\_查询\_FileAlternateNameInformation 的信息请求应响应不包含任何路径信息，该文件的短名称 （8.3 个字符），如果短名称存在该文件。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理查询文件信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
其中的文件或目录的信息是要返回的输出缓冲区的指针。 此信息存储在一个以下结构：

文件\_所有\_信息

文件\_特性\_标记\_信息

文件\_BASIC\_信息

文件\_压缩\_信息

文件\_EA\_信息

文件\_内部\_信息

文件\_名称\_信息

文件\_网络\_打开\_信息

文件\_位置\_信息

文件\_标准\_信息

文件\_流\_信息

文件\_链接\_信息

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)有关接收最终的完成状态和信息的结构请求的操作。 有关详细信息，请参阅的说明*IoStatusBlock*中的参数[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)。 例程。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*可选指向在其中的调用方提供输出缓冲区的内容*Irp-&gt;AssociatedIrp.SystemBuffer* I/O 管理器在 I/O 完成复制。 驱动程序不要使用此缓冲区来返回请求的任何数据。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_查询\_信息和不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_查询\_信息。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*IrpSp-&gt;Parameters.QueryFile.FileInformationClass*要查询文件信息的类型。 此成员可以是下列值之一。

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
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_ALL_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545750" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545750)"> <strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_COMPRESSION_INFORMATION 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>返回该文件的 FILE_EA_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff540318" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540318)"> <strong>FILE_INTERNAL_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff545817" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545817)"> <strong>FILE_NAME_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545822" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545822)"> <strong>FILE_NETWORK_OPEN_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff545855" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545855)"> <strong>FILE_STANDARD_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>返回单个<a href="https://msdn.microsoft.com/library/windows/hardware/ff540364" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540364)"> <strong>FILE_STREAM_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileHardLinkInformation</strong></p></td>
<td align="left"><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff728841" data-raw-source="[&lt;strong&gt;FILE_LINKS_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff728841)"> <strong>FILE_LINKS_INFORMATION</strong> </a>文件的结构。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*IrpSp-&gt;Parameters.QueryFile.Length*指向的缓冲区的长度，以字节为单位， *Irp-&gt;AssociatedIrp.SystemBuffer*。

<a name="remarks"></a>备注
-------

IRP\_MJ\_查询\_信息操作始终缓冲的 I/O 管理器。 *Irp-&gt;AssociatedIrp.SystemBuffer*用于返回所请求的文件或目录信息分配的非分页缓冲池内存中的 I/O 管理器。 因此， *Irp-&gt;AssociatedIrp.SystemBuffer*返回的操作系统将始终为有效的地址中指定的长度作为*IrpSp-&gt;Parameters.QueryFile.Length*.

*Irp-&gt;AssociatedIrp.UserBuffer* I/O 管理器在内部使用和不能由文件系统或文件系统筛选器驱动程序。

## <a name="see-also"></a>另请参阅


[**文件\_对齐\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545740)

[**FILE\_ATTRIBUTE\_TAG\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545750)

[**文件\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**FILE\_INTERNAL\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff540318)

[**文件\_名称\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545817)

[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545822)

[**文件\_位置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**文件\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545855)

[**文件\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**文件\_链接\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff728841)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)

 

 






