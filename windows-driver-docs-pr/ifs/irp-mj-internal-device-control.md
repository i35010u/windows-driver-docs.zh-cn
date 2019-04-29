---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL
ms.assetid: a60325d5-993f-4505-bded-2c2be9782492
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_INTERNAL_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a0ff9e8dbdc77ea427f6f180adf6e932fb7e5d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324321"
---
# <a name="irpmjinternaldevicecontrol"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


## <a name="when-sent"></a>发送时间


IRP\_MJ\_内部\_设备\_控制请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。

与不同[ **IRP\_MJ\_设备\_控制**](irp-mj-device-control.md)请求时，IRP\_MJ\_内部\_设备\_控制请求仅用于内核模式组件之间的通信。 尽管 IRP\_MJ\_设备\_控制请求通常是通过调用**DeviceIoControl**或[ **ZwDeviceIoControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566441)，这些例程不能创建 IRP\_MJ\_内部\_设备\_控制请求。 但是，可以通过调用创建这两种类型的 IRP [ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定是否在表示卷打开的句柄上发出请求的文件对象。 如果这种情况，文件系统驱动程序应将 IRP 传递给在其装载卷的存储设备的设备驱动程序。 如果没有，该驱动程序应失败 IRP。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理和，具体取决于筛选器的特性，完成 IRP 或在堆栈上传递给下一个较低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理设备控制请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向系统提供输入缓冲区要传递到设备驱动程序为目标设备。 用于方法\_缓冲或方法\_直接 I/O。 此参数是否需要取决于特定的 I/O 控制代码。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。 有关详细信息，请参阅的说明*IoStatusBlock*参数[ **ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
描述传递到设备驱动程序为目标设备的输出缓冲区的内存描述符列表 (MDL) 的地址。 用于方法\_直接 I/O。 此参数是否需要取决于特定的 I/O 控制代码。

<a href="" id="irp--requestormode"></a>*Irp-&gt;RequestorMode*  
指示执行模式的进程的请求操作，要么**KernelMode**或**UserMode**。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向要传递到设备驱动程序为目标设备的调用方提供输出缓冲区的指针。 此参数用于方法\_缓冲或方法\_既不 I/O。 此参数是可选的或必需依赖于特定的 I/O 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_内部\_设备\_控件并不应为使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_内部\_设备\_控件。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.InputBufferLength*  
指向以字节为单位的缓冲区的大小*Irp-&gt;AssociatedIrp.SystemBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp-&gt;Parameters.DeviceIoControl.IoControlCode*  
IOCTL 函数代码要传递到设备驱动程序为目标设备。

有关 IOCTL 请求的详细信息，请参阅[使用的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)中*内核模式体系结构指南*和"设备输入和输出控制代码"Microsoft Windows SDK 中文档。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.OutputBufferLength*  
指向以字节为单位的缓冲区的大小*Irp-&gt;UserBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters.DeviceIoControl.Type3InputBuffer*  
对于内核模式下使用方法的输入的缓冲区\_NEITHER。

## <a name="see-also"></a>请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IoGetFunctionCodeFromCtlCode**](https://msdn.microsoft.com/library/windows/hardware/ff549236)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_设备\_控件 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

[使用 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






