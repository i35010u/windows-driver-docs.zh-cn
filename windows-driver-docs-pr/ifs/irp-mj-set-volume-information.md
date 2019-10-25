---
title: IRP_MJ_SET_VOLUME_INFORMATION
description: IRP\_MJ\_设置\_卷\_信息
ms.assetid: 7c317e8b-ffa9-47f7-ac53-23b09873fab9
keywords:
- IRP_MJ_SET_VOLUME_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193450fd1cb3e9844a163a0af323f10de6efa6bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841157"
---
# <a name="irp_mj_set_volume_information"></a>IRP\_MJ\_设置\_卷\_信息


## <a name="when-sent"></a>发送时间


IRP\_MJ\_集\_卷\_信息请求由 i/o 管理器发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如**SetVolumeLabel**）时，可以将其发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是否代表用户卷打开。 如果是这样，则文件系统驱动程序应设置相应的卷信息并完成 IRP。 否则，文件系统应根据需要完成 IRP，而不需要设置卷信息。

可以设置的卷信息的类型与文件系统相关，但通常包括下列一项或多项：

FileFsControlInformation

FileFsLabelInformation

FileFsObjectIdInformation

有关所有可能的信息类型的列表，请参阅 ntifs 中的 FS\_信息\_类枚举。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理设置的卷信息请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向输入缓冲区的指针，该缓冲区包含要设置的卷信息的值。 此信息存储在以下结构之一中：

文件\_FS\_控制\_信息

文件\_FS\_标签\_信息

文件\_FS\_OBJECTID\_信息

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_设置\_卷\_信息时无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*指定 IRP\_MJ\_集\_卷\_信息。

<a href="" id="irpsp--parameters-setvolume-fsinformationclass"></a>*IrpSp-&gt;参数. SetVolume. FsInformationClass*指定要为卷设置的信息类型。 此值可以是下列值之一：

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
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>设置卷的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)"><strong>FILE_FS_CONTROL_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsLabelInformation</strong></p></td>
<td align="left"><p>设置卷的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information" data-raw-source="[&lt;strong&gt;FILE_FS_LABEL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information)"><strong>FILE_FS_LABEL_INFORMATION</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>设置卷的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)"><strong>FILE_FS_OBJECTID_INFORMATION</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setvolume-length"></a>*IrpSp-&gt;参数. SetVolume. 长度*Irp 所指向的缓冲区的长度（以字节为单位） *-&gt;AssociatedIrp. SystemBuffer*。

## <a name="see-also"></a>另请参阅


[**文件\_FS\_控制\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)

[**文件\_FS\_标签\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information)

[**文件\_FS\_OBJECTID\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_查询\_卷\_信息**](irp-mj-query-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






