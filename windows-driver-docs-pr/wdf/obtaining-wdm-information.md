---
title: 获取 WDM 信息
description: 获取 WDM 信息
ms.assetid: a43ffa5b-6166-4624-8dee-a54aaa8c7283
keywords:
- WDM 信息 WDK KMDF
- 状态信息 WDK KMDF WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feed9d5423023203bde627bacc8e4baaa5ed9422
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375062"
---
# <a name="obtaining-wdm-information"></a>获取 WDM 信息


\[仅适用于 KMDF\]

该框架提供多个对象方法，使您的驱动程序以获取 WDM 定义的信息。

### <a name="obtaining-wdm-information-about-the-driver-and-its-devices"></a>获取有关该驱动程序和其设备的 WDM 信息

若要获取 WDM 驱动程序和其设备有关的信息，该驱动程序可以调用以下方法：

<a href="" id="wdffdoinitwdmgetphysicaldevice"></a>[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
检索[ **DEVICE_OBJECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构，它表示设备的物理设备对象 (PDO)。 该驱动程序已创建该设备是 framework 的设备对象之前，驱动程序可以调用此方法。

<a href="" id="wdfdevicewdmgetphysicaldevice"></a>[**WdfDeviceWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetphysicaldevice)  
检索 WDM 设备\_对象结构，它表示设备的 PDO。 创建设备是 framework 的设备对象后，驱动程序可以调用此方法。

<a href="" id="wdfdevicewdmgetdeviceobject"></a>[**WdfDeviceWdmGetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)  
返回与指定的框架设备对象相关联的 WDM 设备对象。

<a href="" id="wdfdevicewdmgetattacheddevice"></a>[**WdfDeviceWdmGetAttachedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetattacheddevice)  
返回下一步低 WDM 设备对象中的[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)。

<a href="" id="wdfwdmdevicegetwdfdevicehandle"></a>[**WdfWdmDeviceGetWdfDeviceHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfwdmdevicegetwdfdevicehandle)  
返回与指定的 WDM 设备对象相关联的 framework 设备对象的句柄。

<a href="" id="wdfwdmdrivergetwdfdriverhandle"></a>[**WdfWdmDriverGetWdfDriverHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfwdmdrivergetwdfdriverhandle)  
返回与指定的 WDM 驱动程序对象相关联的 framework 驱动程序对象的句柄。

### <a name="obtaining-wdm-information-about-io-requests"></a>获取有关输入/输出请求的 WDM 信息

若要获取有关输入/输出请求的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfrequestwdmgetirp"></a>[**WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)  
返回 WDM [ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)结构，它是与指定的框架请求对象相关联。 (另一方面，接收框架外部 WDM IRP 的驱动程序可以创建一个框架请求对象的 IRP 通过调用[ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)。)

<a href="" id="wdfrequestgetparameters"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
检索与指定的框架请求对象相关联的参数。 这些参数来自请求的 WDM [I/O 堆栈位置](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)。)

<a href="" id="wdfrequestretrieveoutputwdmmdl"></a>[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)  
检索表示 I/O 请求的输出缓冲区的内存描述符列表 (MDL)。

<a href="" id="wdfrequestretrieveinputwdmmdl"></a>[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)  
检索表示 I/O 请求的输入的缓冲区 MDL。

<a href="" id="wdfrequestformatrequestusingcurrenttype"></a>[**WdfRequestFormatRequestUsingCurrentType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)  
将调用驱动程序的 I/O 堆栈位置的内容复制到驱动程序的本地 I/O 目标的 I/O 堆栈位置。

<a href="" id="wdfrequestwdmformatusingstacklocation"></a>[**WdfRequestWdmFormatUsingStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation)  
设置驱动程序的本地 I/O 目标的 I/O 堆栈位置的内容。

### <a name="obtaining-wdm-information-about-io-targets"></a>获取有关 I/O 目标 WDM 信息

若要获取 WDM I/O 目标的信息，请将驱动程序可以调用以下方法：

<a href="" id="wdfiotargetwdmgettargetdeviceobject"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
返回一个指向与本地或远程 I/O 目标相关联的 WDM 设备对象。

<a href="" id="wdfiotargetwdmgettargetfileobject"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
返回一个指向 WDM [**文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)结构，它是与远程 I/O 目标相关联。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
返回的句柄与远程 I/O 目标相关联的文件。

<a href="" id="wdfiotargetwdmgettargetphysicaldevice"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
返回一个指向 WDM 物理设备 (PDO) 对象，该对象表示远程 I/O 目标设备。

### <a name="obtaining-wdm-information-about-interrupts-and-dpcs"></a>获取有关中断和 dpc 进行标记的 WDM 信息

若要获取 WDM 有关中断和延缓的过程调用 (Dpc) 的信息，请将驱动程序可以调用以下方法：

<a href="" id="wdfinterruptwdmgetinterrupt"></a>[**WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)  
返回一个指向 WDM [ **KINTERRUPT** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，它是与指定的框架中断对象相关联。

<a href="" id="wdfdpcwdmgetdpc"></a>[**WdfDpcWdmGetDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcwdmgetdpc)  
返回一个指向 WDM [ **KDPC** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构，它是与指定的框架 DPC 对象相关联。

### <a href="" id="obtaining-wdm-information-about-usb-i-o-targets"></a> 获取有关 USB I/O 目标 WDM 信息

若要获取有关 USB I/O 目标 WDM 信息，请将驱动程序可以调用以下方法：

<a href="" id="wdfusbtargetpipewdmgetpipehandle"></a>[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
返回 USBD\_管道\_句柄类型的句柄与指定的框架管道对象相关联。

### <a name="obtaining-wdm-information-about-the-registry"></a>获取有关注册表的 WDM 信息

若要获取有关注册表的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfregistrywdmgethandle"></a>[**WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)  
返回的 WDM 句柄 framework 注册表项对象表示的注册表项。

### <a name="obtaining-wdm-information-about-file-objects"></a>获取有关文件对象的 WDM 信息

若要获取 WDM 文件对象的信息，请将驱动程序可以调用以下方法：

<a href="" id="wdffileobjectwdmgetfileobject"></a>[**WdfFileObjectWdmGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
返回 WDM [**文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)结构，它是与指定的框架文件对象相关联。

 

 





