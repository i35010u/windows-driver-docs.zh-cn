---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP\_MJ\_FILE\_SYSTEM\_CONTROL
ms.assetid: 9df42b58-5820-44fd-8e55-0195807be951
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_FILE_SYSTEM_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 961bcb465af3150829a5e9bee1ee28b2d42ac47e
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464339"
---
# <a name="irpmjfilesystemcontrol"></a>IRP\_MJ\_FILE\_SYSTEM\_CONTROL


## <a name="when-sent"></a>发送时间


IRP\_MJ\_文件\_系统\_控制请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 它可以发送，例如，当用户模式应用程序已调用 Microsoft Win32 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)函数来发送文件系统 I/O 控制 (FSCTL) 请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序或识别器应检查次要函数代码，以确定请求的文件系统控制操作。

文件系统驱动程序应处理以下次要函数代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_KERNEL_CALL</p></td>
<td align="left"><p>此请求是 IRP_MN_USER_FS_REQUEST 相同 （介绍以下），只不过请求的源是一个受信任的内核组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_MOUNT_VOLUME</p></td>
<td align="left"><p>指示卷装入请求。 如果文件系统驱动程序收到此 IRP 的格式不匹配的文件系统卷，文件系统驱动程序应返回 STATUS_UNRECOGNIZED_VOLUME。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_USER_FS_REQUEST</p></td>
<td align="left"><p>指示一个 FSCTL 请求，可能是代表已调用 Microsoft Win32 DeviceIoControl 函数的用户模式应用程序或具有名为一个内核模式组件代表<a href="https://msdn.microsoft.com/library/windows/hardware/ff566441" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566441)"> <strong>ZwDeviceIoControlFile</strong></a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong></a>。</p>
<p>有关 FSCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的"设备输入和输出控制代码"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_VERIFY_VOLUME</p></td>
<td align="left"><p>指示卷验证请求。 对于可移动介质，文件系统必须验证该卷时检测到已删除并返回，以确保它仍然是以前使用文件系统的同一个卷媒体。 如果该卷已更改，文件系统应使所有未完成的句柄无效。 仅在此新的介质上的文件系统已更改时，它也将返回错误。 此请求是最常用于软盘驱动器。</p></td>
</tr>
</tbody>
</table>

 

文件系统的识别器必须处理以下次要函数代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_LOAD_FILE_SYSTEM</p></td>
<td align="left"><p>指示加载文件系统请求。</p></td>
</tr>
</tbody>
</table>

 

在执行请求的操作之后, 的文件系统驱动程序或识别器应完成 IRP。

## <a name="operation-files-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理文件系统控制请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向系统提供输入缓冲区传递到文件系统或文件系统筛选器驱动程序的目标卷。 用于方法\_缓冲或方法\_直接 I/O。 此参数是否需要取决于特定文件系统控制代码。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
内存描述符列表 (MDL) 描述要传递到文件系统或文件系统筛选器驱动程序的目标卷的输出缓冲区的地址。 用于方法\_直接 I/O。 此参数是否需要取决于特定的 I/O 控制代码。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向要传递到文件系统或文件系统筛选器驱动程序的目标卷的调用方提供输出缓冲区的指针。 用于方法\_缓冲或方法\_既不 I/O。 此参数是可选的或必需依赖于特定的 I/O 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_文件\_系统\_控件，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  
以下标志可设置为 IRP\_MN\_验证\_卷：

SL\_允许\_RAW\_装载

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_文件\_系统\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_KERNEL\_CALL
-   IRP\_MN\_LOAD\_FILE\_SYSTEM
-   IRP\_MN\_装载\_卷
-   IRP\_MN\_USER\_FS\_REQUEST
-   IRP\_MN\_验证\_卷

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp-&gt;Parameters.FileSystemControl.FsControlCode*  
要传递到文件系统或文件系统筛选器驱动程序的目标卷的 FSCTL 函数代码。 用于 IRP\_MN\_用户\_FS\_仅请求。

IOCTL 和 FSCTL 请求有关的详细信息，请参阅[使用的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)中*内核模式体系结构指南*和"设备输入和输出控制代码"Microsoft Windows SDK 中文档。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters.FileSystemControl.InputBufferLength*  
指向以字节为单位的缓冲区的大小*Irp-&gt;AssociatedIrp.SystemBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters.FileSystemControl.OutputBufferLength*  
指向以字节为单位的缓冲区的大小*Irp-&gt;UserBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters.FileSystemControl.Type3InputBuffer*  
对于内核模式下使用方法的输入的缓冲区\_NEITHER。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp-&gt;Parameters.MountVolume.DeviceObject*  
指向实际设备的卷是要装载的设备对象指针。 文件系统筛选器驱动程序不应使用此参数。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp-&gt;Parameters.MountVolume.Vpb*  
指向要装载的卷的卷参数块 (VPB)。 支持可移动介质的文件系统可能用此参数中传递的一个以前用过 VPB。 此类文件在系统上，装载卷后，此指针可以被认为有效。 文件系统筛选器驱动程序筛选这些文件系统应使用此参数，如下所示：筛选器应发送到较低级别的驱动程序 IRP 之前, 保存的值*IrpSp-&gt;Parameters.MountVolume.Vpb-&gt;RealDevice*。 已成功装载卷后，筛选器可以使用此指针，指向存储设备对象以获取正确的 VPB 指针。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp-&gt;Parameters.VerifyVolume.DeviceObject*  
指向要验证的卷的设备对象指针。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp-&gt;Parameters.VerifyVolume.Vpb*  
指向卷 VPB，若要进行验证。

## <a name="see-also"></a>请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






