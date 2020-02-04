---
title: IRP_MJ_DEVICE_CONTROL
description: IRP\_MJ\_DEVICE\_CONTROL
ms.assetid: 7a7f7372-ed69-42c1-95e2-b5a593d77d22
keywords:
- IRP_MJ_DEVICE_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f6d9682a343737cb3d2fb0a90cf11be066afb3
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977684"
---
# <a name="irp_mj_device_control"></a>IRP\_MJ\_DEVICE\_CONTROL


## <a name="when-sent"></a>发送时间


IRP\_MJ\_设备\_控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 通常，此 IRP 代表用户模式应用程序发送，该应用程序已调用 Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数或代表已调用[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)的内核模式组件。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定是否已在打开的句柄上发出请求。 如果是这种情况，则文件系统驱动程序应将 IRP 传递到用于装入卷的存储设备的设备驱动程序。 否则，该驱动程序应该会使 IRP 失败。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，完成 IRP，或将其向下传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序为给定的 IRP 调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理设备控制请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区将传递给目标设备的设备驱动程序。 用于方法\_\_直接 i/o 的缓冲或方法。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)的*IoStatusBlock*参数说明。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
描述要传递到目标设备的设备驱动程序的输出缓冲区的内存描述符列表（MDL）的地址。 用于方法\_直接 i/o。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--requestormode"></a>*Irp-&gt;Irp->requestormode*  
指示请求操作的进程的执行模式，可以是**KernelMode**或**UserMode**。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
一个指针，指向要传递给目标设备的设备驱动程序的调用方提供的输出缓冲区。 用于方法\_缓冲或方法\_i/o 都不是。 此参数是可选的还是必需的取决于特定的 i/o 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_设备\_控制期间无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_设备\_控件。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp-&gt;参数. DeviceIoControl. InputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） *-&gt;AssociatedIrp. SystemBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp-&gt;参数. DeviceIoControl. IoControlCode*  
要传递给目标设备的设备驱动程序的 IOCTL 函数代码。

有关 IOCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp-&gt;参数. DeviceIoControl. OutputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） *&gt;UserBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp-&gt;参数. DeviceIoControl. Type3InputBuffer*  
使用方法\_的内核模式请求的输入缓冲区均不是。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IoGetFunctionCodeFromCtlCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetfunctioncodefromctlcode)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_设备\_控制（WDK 内核参考）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

[使用 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






