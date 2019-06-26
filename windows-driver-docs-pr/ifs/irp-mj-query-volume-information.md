---
title: IRP_MJ_QUERY_VOLUME_INFORMATION
description: IRP\_MJ\_查询\_卷\_信息
ms.assetid: 1e762c75-70bd-4397-b244-df97b317b3bf
keywords:
- IRP_MJ_QUERY_VOLUME_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ead50b6913b1915b67aa4c8941885f5bd4003db6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384814"
---
# <a name="irpmjqueryvolumeinformation"></a>IRP\_MJ\_查询\_卷\_信息


## <a name="when-sent"></a>发送时间


**IRP\_MJ\_查询\_卷\_信息**I/O 管理器发送请求。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**GetDiskFreeSpace**或**GetFileType**。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定目标设备对象是否为文件系统控制设备对象的文件对象。 如果是，并已打开的卷 （或一种开放的卷上的对象） 句柄上发出请求，文件系统驱动程序应处理该请求，并完成 IRP。

否则为文件系统驱动程序应查询将失败，并完成 IRP。

可以查询的卷信息的类型是文件系统相关，但通常包括以下各项：

FileFsAttributeInformation

FileFsDeviceInformation

FileFsSizeInformation

FileFsVolumeInformation

有关所有可能的信息类型的列表，请参阅*IrpSp-&gt;Parameters.QueryVolume.FsInformationClass*下面。

## <a name="operation-network-redirect-drivers"></a>操作：网络重定向驱动程序


收到请求时为 FileFsDeviceInformation，网络重定向程序必须包括文件\_远程\_设备的选项之一**DeviceCharacteristics**的成员[ **文件\_FS\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)返回结构。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理查询卷信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
到其中的卷信息是要返回的系统提供的输出缓冲区的指针。 此信息存储在一个以下结构：

文件\_FS\_属性\_信息

文件\_FS\_控制\_信息

文件\_FS\_设备\_信息

文件\_FS\_驱动程序\_路径\_信息

文件\_FS\_完整\_大小\_信息

文件\_FS\_OBJECTID\_信息

文件\_FS\_大小\_信息

文件\_FS\_卷\_标志\_信息

文件\_FS\_卷\_信息

文件\_FS\_扇区\_大小\_信息

FileFsVolumeFlagsInformation 类和关联[**文件\_FS\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)结构是适用于 Windows Vista 及更高版本版本。

<a href="" id="------irp--iostatus"></a> *Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)有关接收最终的完成状态和信息的结构请求的操作。

<a href="" id="------irp--userbuffer"></a> *Irp-&gt;UserBuffer*可选指向在其中的调用方提供输出缓冲区的内容*Irp-&gt;AssociatedIrp.SystemBuffer* I/O 管理器在 I/O 完成复制。 驱动程序不要使用此缓冲区来返回请求的任何数据。

<a href="" id="------irpsp--fileobject"></a> *IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的处理过程**IRP\_MJ\_查询\_卷\_信息**，不应使用。

<a href="" id="------irpsp--majorfunction"></a> *IrpSp-&gt;MajorFunction*指定**IRP\_MJ\_查询\_卷\_信息**。

<a href="" id="------irpsp--parameters-queryvolume-fsinformationclass"></a> *IrpSp-&gt;Parameters.QueryVolume.FsInformationClass*指定返回文件系统卷信息的类型。 此成员可以是以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileFsAttributeInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information" data-raw-source="[&lt;strong&gt;FILE_FS_ATTRIBUTE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information)"> <strong>FILE_FS_ATTRIBUTE_INFORMATION</strong> </a>结构，其中包含有关文件系统负责该卷的属性信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>结构，其中包含有关卷的文件系统控制信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsDeviceInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)"> <strong>FILE_FS_DEVICE_INFORMATION</strong> </a>结构，其中包含该卷的设备信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsDriverPathInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information)"> <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> </a>结构，其中包含有关指定驱动程序是在该卷的 I/O 路径信息。 创建者<strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>请求必须存储到驱动程序的名称<strong>FILE_FS_DRIVER_PATH_INFORMATION</strong>之前将 IRP 发送到文件系统的结构卷设备堆栈。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsFullSizeInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information)"> <strong>FILE_FS_FULL_SIZE_INFORMATION</strong> </a>结构，其中包含有关在卷上的总可用空间量的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>结构，其中包含该卷的特定于系统文件的对象 ID 信息。 请注意，这是不由操作系统分配的 （基于 GUID 的） 唯一卷名称相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSizeInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information)"> <strong>FILE_FS_SIZE_INFORMATION</strong> </a>结构，它包含有关可供用户使用与发出线程关联的卷上的空间量的信息<strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsVolumeInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a> ，包含有关卷的卷标签、 序列号和创建时间等信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSectorSizeInformation</strong></p></td>
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_sector_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_sector_size_information)"> <strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong> </a>结构，其中包含有关物理和逻辑扇区大小的卷的信息。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="------irpsp--parameters-queryvolume-length"></a> *IrpSp-&gt;Parameters.QueryVolume.Length*指向的缓冲区的长度，以字节为单位， *Irp-&gt;UserBuffer*。 返回时，此变量接收到的缓冲区写入的字节数。

## <a name="see-also"></a>请参阅


[**文件\_FS\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information)

[**文件\_FS\_控制\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)

[**FILE\_FS\_DEVICE\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)

[**文件\_FS\_驱动程序\_路径\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information)

[**文件\_FS\_完整\_大小\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information)

[**文件\_FS\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)

**文件\_FS\_扇区\_大小\_信息**
[**文件\_FS\_大小\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information)

[**文件\_FS\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_设置\_卷\_信息**](irp-mj-set-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






