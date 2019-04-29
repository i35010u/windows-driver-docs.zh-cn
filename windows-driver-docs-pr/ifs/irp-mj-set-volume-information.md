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
ms.openlocfilehash: c28f85258d1af00cd199d1880af78a7dde7bf122
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324488"
---
# <a name="irpmjsetvolumeinformation"></a>IRP\_MJ\_设置\_卷\_信息


## <a name="when-sent"></a>发送时间


IRP\_MJ\_设置\_卷\_信息请求发送的 I/O 管理器。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**SetVolumeLabel**。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定它是否表示用户卷打开的文件对象。 如果是这样，文件系统驱动程序应该能够设置适当的卷信息并完成 IRP。 否则，文件系统应完成根据 IRP，而无需设置的卷信息。

可以设置的卷信息的类型是文件系统相关，但一般都包括一个或多个以下：

FileFsControlInformation

FileFsLabelInformation

FileFsObjectIdInformation

有关所有可能的信息类型的列表，请参阅 FS\_信息\_中 ntifs.h 类枚举。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理组卷信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向包含要设置的卷信息的值的输入缓冲区的指针。 此信息存储在一个以下结构：

文件\_FS\_控制\_信息

文件\_FS\_标签\_信息

文件\_FS\_OBJECTID\_信息

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)有关接收最终的完成状态和信息的结构请求的操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_设置\_卷\_信息并且不应是使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_设置\_卷\_信息。

<a href="" id="irpsp--parameters-setvolume-fsinformationclass"></a>*IrpSp-&gt;Parameters.SetVolume.FsInformationClass*指定要为卷设置的信息类型。 此值可以是以下值之一：

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
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540258" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540258)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>卷。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsLabelInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540271" data-raw-source="[&lt;strong&gt;FILE_FS_LABEL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540271)"> <strong>FILE_FS_LABEL_INFORMATION</strong> </a>卷。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>设置<a href="https://msdn.microsoft.com/library/windows/hardware/ff540274" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540274)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>卷。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setvolume-length"></a>*IrpSp-&gt;Parameters.SetVolume.Length*指向的缓冲区的长度，以字节为单位， *Irp-&gt;AssociatedIrp.SystemBuffer*。

## <a name="see-also"></a>请参阅


[**文件\_FS\_控制\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540258)

[**文件\_FS\_标签\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540271)

[**文件\_FS\_OBJECTID\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540274)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_查询\_卷\_信息**](irp-mj-query-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






