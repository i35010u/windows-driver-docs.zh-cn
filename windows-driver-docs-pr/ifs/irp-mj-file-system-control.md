---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP\_MJ\_文件\_系统\_控件
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
ms.openlocfilehash: ee15f03741b6c0c730e4bd387f10306c720f2940
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841193"
---
# <a name="irp_mj_file_system_control"></a>IRP\_MJ\_文件\_系统\_控件


## <a name="when-sent"></a>发送时间


IRP\_MJ\_文件\_系统\_控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，可以在用户模式应用程序调用 Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数来发送文件系统 i/o 控制（FSCTL）请求时发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序或识别器应检查次要函数代码以确定请求了哪个文件系统控制操作。

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
<td align="left"><p>此请求与 IRP_MN_USER_FS_REQUEST （如下所述）相同，不同之处在于请求的源是可信内核组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_MOUNT_VOLUME</p></td>
<td align="left"><p>指示卷装入请求。 如果文件系统驱动程序接收到其格式与文件系统格式不匹配的卷的此 IRP，则文件系统驱动程序应返回 STATUS_UNRECOGNIZED_VOLUME。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_USER_FS_REQUEST</p></td>
<td align="left"><p>指示一个 FSCTL 请求，该请求可能代表一个用户模式应用程序，该应用程序调用了 Microsoft Win32 DeviceIoControl 函数或代表一个已调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff566441" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566441)"><strong>ZwDeviceIoControlFile</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>的内核模式组件IoBuildDeviceIoControlRequest</strong></a>。</p>
<p>有关 FSCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的 "设备输入和输出控制代码"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_VERIFY_VOLUME</p></td>
<td align="left"><p>指示卷验证请求。 对于可移动媒体，文件系统在检测到已删除并返回媒体时必须验证卷，以确保它仍与文件系统以前使用的卷相同。 如果卷已更改，则文件系统应使所有未完成的句柄无效。 如果此新介质上的文件系统已更改，它也会返回错误。 此请求最常用于软盘驱动器。</p></td>
</tr>
</tbody>
</table>

 

文件系统识别器必须处理以下次要函数代码：

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

 

执行请求的操作后，文件系统驱动程序或识别器应完成 IRP。

## <a name="operation-files-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用在处理文件系统控制请求中的以下 IRP 成员和 IRP 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区将传递给目标卷的文件系统或文件系统筛选器驱动程序。 用于方法\_\_直接 i/o 的缓冲或方法。 此参数是否是必需的取决于特定的文件系统控制代码。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
内存描述符列表（MDL）的地址，描述要传递到目标卷的文件系统或文件系统筛选器驱动程序的输出缓冲区。 用于方法\_直接 i/o。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
一个指针，指向要传递给目标卷的文件系统或文件系统筛选器驱动程序的调用方提供的输出缓冲区。 用于方法\_缓冲或方法\_i/o 都不是。 此参数是可选的还是必需的取决于特定的 i/o 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_文件\_SYSTEM\_控件期间无效，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;标志*  
可以为 IRP\_MN\_验证\_卷设置以下标志：

SL\_允许\_RAW\_装载

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_文件\_系统\_控件。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
下列情况之一：

-   IRP\_MN\_内核\_调用
-   IRP\_MN\_加载\_文件\_系统
-   IRP\_MN\_装载\_卷
-   IRP\_MN\_用户\_FS\_请求
-   IRP\_MN\_验证\_卷

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp-&gt;参数. FileSystemControl. FsControlCode*  
要传递给目标卷的文件系统或文件系统筛选器驱动程序的 FSCTL 函数代码。 仅适用于 IRP\_MN\_USER\_FS\_请求。

有关 IOCTL 和 FSCTL 请求的详细信息，请参阅在 Microsoft Windows SDK 文档中使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp-&gt;参数. FileSystemControl. InputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） *-&gt;AssociatedIrp. SystemBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp-&gt;参数. FileSystemControl. OutputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） *&gt;UserBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp-&gt;参数. FileSystemControl. Type3InputBuffer*  
使用方法\_的内核模式请求的输入缓冲区均不是。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp-&gt;参数. MountVolume. DeviceObject*  
一个指针，指向要在其上装载卷的实际设备的设备对象。 文件系统筛选器驱动程序不应使用此参数。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp-&gt;参数. MountVolume. Vpb*  
一个指针，指向要装入的卷的卷参数块（VPB）。 支持可移动媒体的文件系统可能会将以前使用过的 VPB 替换为此参数中传递的文件系统。 在此类文件系统上，在装入卷后，不能再将此指针视为有效。 筛选这些文件系统的文件系统筛选器驱动程序应使用此参数，如下所示：在将 IRP 发送到较低级别的驱动程序之前，筛选器应将*IrpSp-&gt;参数的值保存&gt;Vpb-RealDevice*。 成功装入卷后，筛选器可以使用指向存储设备对象的指针来获取正确的 VPB 指针。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp-&gt;参数. VerifyVolume. DeviceObject*  
一个指针，指向要验证的卷的设备对象。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp-&gt;参数. VerifyVolume. Vpb*  
指向要验证的卷的 VPB 的指针。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






