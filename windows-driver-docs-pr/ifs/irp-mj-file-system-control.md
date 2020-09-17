---
title: 'IRP_MJ_FILE_SYSTEM_CONTROL (IFS) '
description: IRP \_ MJ \_ 文件 \_ 系统 \_ 控制
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
ms.openlocfilehash: 7cea04b8680e325afe6481f4aa42f9e904839c2d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715626"
---
# <a name="irp_mj_file_system_control-ifs"></a>\_ (IFS) 的 IRP MJ \_ 文件 \_ 系统 \_ 控制


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 文件 \_ 系统 \_ 控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，可以在用户模式应用程序调用 Microsoft Win32 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数以将文件系统 i/o 控制发送 (FSCTL) 请求时发送。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_KERNEL_CALL</p></td>
<td align="left"><p>此请求与以下) 所述 (IRP_MN_USER_FS_REQUEST 相同，不同之处在于请求源是受信任的内核组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_MOUNT_VOLUME</p></td>
<td align="left"><p>指示卷装入请求。 如果文件系统驱动程序接收到其格式与文件系统格式不匹配的卷的此 IRP，则文件系统驱动程序应返回 STATUS_UNRECOGNIZED_VOLUME。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_USER_FS_REQUEST</p></td>
<td align="left"><p>指示一个 FSCTL 请求，该请求可能代表一个用户模式应用程序，该应用程序调用了 Microsoft Win32 DeviceIoControl 函数或代表一个已调用 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwdeviceiocontrolfile" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwdeviceiocontrolfile)"><strong>ZwDeviceIoControlFile</strong></a> 或 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>的内核模式组件。</p>
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
<th align="left">说明</th>
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


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理文件系统控制请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区将传递给目标卷的文件系统或文件系统筛选器驱动程序。 用于方法 \_ 缓冲或方法 \_ 直接 i/o。 此参数是否是必需的取决于特定的文件系统控制代码。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  
 (MDL 的内存描述符列表的地址) 描述要传递到文件系统的输出缓冲区或目标卷的文件系统筛选器驱动程序。 用于方法 \_ 直接 i/o。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
一个指针，指向要传递给目标卷的文件系统或文件系统筛选器驱动程序的调用方提供的输出缓冲区。 用于方法 \_ 缓冲或方法 \_ 都不是 i/o。 此参数是可选的还是必需的取决于特定的 i/o 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject*关联的文件对象的指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ \_ 文件系统控件期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; 标志*  
可以为 IRP \_ MN 验证卷设置以下标志 \_ \_ ：

SL \_ 允许 \_ 原始 \_ 装载

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 文件 \_ 系统 \_ 控制。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; MinorFunction*  
下列类型作之一：

-   IRP \_ MN \_ 内核 \_ 调用
-   IRP \_ MN \_ 加载 \_ 文件 \_ 系统
-   IRP \_ MN \_ 装入 \_ 卷
-   IRP \_ MN \_ 用户 \_ FS \_ 请求
-   IRP \_ MN \_ 验证 \_ 卷

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp- &gt; FileSystemControl. FsControlCode*  
要传递给目标卷的文件系统或文件系统筛选器驱动程序的 FSCTL 函数代码。 仅用于 IRP \_ MN \_ USER \_ FS \_ 请求。

有关 IOCTL 和 FSCTL 请求的详细信息，请参阅在 Microsoft Windows SDK 文档中使用*内核模式体系结构指南*中的[i/o 控制代码](../kernel/introduction-to-i-o-control-codes.md)和 "设备输入和输出控制代码"。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp- &gt; FileSystemControl. InputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） * &gt;AssociatedIrp.SystemBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp- &gt; FileSystemControl. OutputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位）。 * &gt; UserBuffer*。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp- &gt; FileSystemControl. Type3InputBuffer*  
使用方法的内核模式请求的输入缓冲区 \_ 均不是。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp- &gt; MountVolume. DeviceObject*  
一个指针，指向要在其上装载卷的实际设备的设备对象。 文件系统筛选器驱动程序不应使用此参数。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp- &gt; MountVolume. Vpb*  
指向卷参数块的指针 (要装入的卷的 VPB) 。 支持可移动媒体的文件系统可能会将以前使用过的 VPB 替换为此参数中传递的文件系统。 在此类文件系统上，在装入卷后，不能再将此指针视为有效。 筛选这些文件系统的文件系统筛选器驱动程序应使用此参数，如下所示：在将 IRP 发送到较低级别的驱动程序之前，筛选器应保存 *IrpSp- &gt; MountVolume. Vpb- &gt; RealDevice*的值。 成功装入卷后，筛选器可以使用指向存储设备对象的指针来获取正确的 VPB 指针。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp- &gt; VerifyVolume. DeviceObject*  
一个指针，指向要验证的卷的设备对象。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp- &gt; VerifyVolume. Vpb*  
指向要验证的卷的 VPB 的指针。

## <a name="see-also"></a>请参阅


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**ZwDeviceIoControlFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwdeviceiocontrolfile)