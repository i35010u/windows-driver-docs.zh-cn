---
title: IRP_MJ_QUERY_VOLUME_INFORMATION
description: IRP \_ MJ \_ 查询 \_ 卷 \_ 信息
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
ms.openlocfilehash: de3bbd198d2609b3e58833acb15f852ea0457bd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793781"
---
# <a name="irp_mj_query_volume_information"></a>IRP \_ MJ \_ 查询 \_ 卷 \_ 信息


## <a name="when-sent"></a>发送时间


**IRP \_ MJ \_ 查询 \_ 卷 \_ 信息** 请求由 i/o 管理器发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **GetDiskFreeSpace** 或 **GetFileType**）时，可以发送它。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定目标设备对象是否为文件系统的控制设备对象。 如果是，并且如果请求是在打开的某个卷的句柄上发出 (或) 上的对象打开，则文件系统驱动程序应处理该请求并完成 IRP。

否则，文件系统驱动程序应使查询失败并完成 IRP。

可以查询的卷信息的类型与文件系统相关，但通常包括：

FileFsAttributeInformation

FileFsDeviceInformation

FileFsSizeInformation

FileFsVolumeInformation

有关所有可能的信息类型的列表，请参阅下面的 *IrpSp- &gt; QueryVolume. FsInformationClass* 。

## <a name="operation-network-redirect-drivers"></a>操作：网络重定向驱动程序


接收 FileFsDeviceInformation 请求的网络重定向程序必须包含文件 \_ 远程设备， \_ 作为返回的 [**文件 \_ FS \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)结构的 **DeviceCharacteristics** 成员的一个选项。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理查询卷信息请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
指向系统提供的输出缓冲区的指针，将在其中返回卷信息。 此信息存储在以下结构之一中：

文件 \_ FS \_ 属性 \_ 信息

文件 \_ FS \_ 控制 \_ 信息

文件 \_ FS \_ 设备 \_ 信息

文件 \_ FS \_ 驱动程序 \_ 路径 \_ 信息

文件 \_ FS \_ 完整 \_ 大小 \_ 信息

文件 \_ FS \_ OBJECTID \_ 信息

文件 \_ FS \_ 大小 \_ 信息

文件 \_ FS \_ 卷 \_ 标志 \_ 信息

文件 \_ FS \_ 卷 \_ 信息

文件 \_ FS \_ 扇区 \_ 大小 \_ 信息

Windows Vista 和更高版本中提供了 FileFsVolumeFlagsInformation 类和关联的 [**文件 \_ FS \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information) 结构。

<a href="" id="------irp--iostatus"></a>*Irp- &gt;IoStatus* 指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="------irp--userbuffer"></a>*Irp- &gt;UserBuffer* 可选指针，指向调用方提供的输出缓冲区，在 i/o 管理器的 i/o 完成过程中，会将 *Irp &gt;AssociatedIrp.SystemBuffer* 的内容复制到其中。 驱动程序不使用此缓冲区返回请求的任何数据。

<a href="" id="------irpsp--fileobject"></a>*IrpSp- &gt;* 指向与 *DeviceObject* 关联的文件对象的 FileObject 指针。

*IrpSp- &gt; FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 **IRP \_ MJ \_ 查询 \_ 卷 \_ 信息** 期间无效，不应使用。

<a href="" id="------irpsp--majorfunction"></a>*IrpSp- &gt;MajorFunction* 指定 **IRP \_ MJ \_ 查询 \_ 卷 \_ 信息**。

<a href="" id="------irpsp--parameters-queryvolume-fsinformationclass"></a>*IrpSp- &gt;QueryVolume. FsInformationClass* 指定文件系统要返回的卷信息的类型。 此成员可以是以下项之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileFsAttributeInformation</strong></p></td>
<td align="left"><p>返回一个 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information" data-raw-source="[&lt;strong&gt;FILE_FS_ATTRIBUTE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information)"><strong>FILE_FS_ATTRIBUTE_INFORMATION</strong></a> 结构，该结构包含有关负责卷的文件系统的属性信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>返回一个 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)"><strong>FILE_FS_CONTROL_INFORMATION</strong></a> 结构，该结构包含有关卷的文件系统控制信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsDeviceInformation</strong></p></td>
<td align="left"><p>返回 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)"><strong>FILE_FS_DEVICE_INFORMATION</strong></a> 结构，该结构包含卷的设备信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsDriverPathInformation</strong></p></td>
<td align="left"><p>返回一个 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)"><strong>FILE_FS_DRIVER_PATH_INFORMATION</strong></a> 结构，该结构包含有关指定的驱动程序是否位于该卷的 i/o 路径中的信息。 在将 IRP 发送到文件系统卷设备堆栈之前， <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong> 请求的发起方必须将驱动程序的名称存储到 <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> 结构中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsFullSizeInformation</strong></p></td>
<td align="left"><p>返回 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information)"><strong>FILE_FS_FULL_SIZE_INFORMATION</strong></a> 结构，该结构包含有关卷上可用空间总量的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>返回 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)"><strong>FILE_FS_OBJECTID_INFORMATION</strong></a> 结构，该结构包含卷的特定于文件的对象 ID 信息。 请注意，这与操作系统分配的 (基于 GUID 的) 唯一卷名称不同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSizeInformation</strong></p></td>
<td align="left"><p>返回一个 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information)"><strong>FILE_FS_SIZE_INFORMATION</strong></a> 结构，该结构包含有关卷上的空间量的信息，该信息可供与发出 <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong> 请求的线程关联的用户使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsVolumeInformation</strong></p></td>
<td align="left"><p>返回一个 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)"><strong>FILE_FS_VOLUME_INFORMATION</strong></a> ，其中包含有关卷的信息，例如卷标、序列号和创建时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSectorSizeInformation</strong></p></td>
<td align="left"><p>返回 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_sector_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_sector_size_information)"><strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong></a> 结构，该结构包含有关卷的物理扇区大小和逻辑扇区大小的信息。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="------irpsp--parameters-queryvolume-length"></a>*IrpSp- &gt;* *&gt; UserBuffer* 所指向的缓冲区的 QueryVolume 长度（以字节为单位）。 返回时，此变量将接收写入缓冲区的字节数。

## <a name="see-also"></a>请参阅


[**文件 \_ FS \_ 属性 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information)

[**文件 \_ FS \_ 控制 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)

[**文件 \_ FS \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)

[**文件 \_ FS \_ 驱动程序 \_ 路径 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)

[**文件 \_ FS \_ 完整 \_ 大小 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information)

[**文件 \_ FS \_ OBJECTID \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)

**文件 \_FS \_ 扇区 \_ 大小 \_ 信息** 
 [**文件 \_ FS \_ 大小 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information)

[**文件 \_ FS \_ 卷 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设置 \_ 卷 \_ 信息**](irp-mj-set-volume-information.md)

[**ZwQueryVolumeInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwqueryvolumeinformationfile)

[**ZwSetVolumeInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwsetvolumeinformationfile)

