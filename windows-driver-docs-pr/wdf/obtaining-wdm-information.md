---
title: 获取 WDM 信息
description: 获取 WDM 信息
ms.assetid: a43ffa5b-6166-4624-8dee-a54aaa8c7283
keywords:
- WDM 信息 WDK KMDF
- 状态信息 WDK KMDF，WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6d60763fd59222e41df36f762624431edfbe74c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844799"
---
# <a name="obtaining-wdm-information"></a>获取 WDM 信息


\[仅适用于 KMDF\]

该框架提供了若干对象方法，使您的驱动程序能够获取 WDM 定义的信息。

### <a name="obtaining-wdm-information-about-the-driver-and-its-devices"></a>获取有关驱动程序及其设备的 WDM 信息

若要获取有关驱动程序及其设备的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdffdoinitwdmgetphysicaldevice"></a>[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
检索表示设备的物理设备对象（PDO）的[**DEVICE_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构。 驱动程序可以在驱动程序为设备创建框架设备对象之前调用此方法。

<a href="" id="wdfdevicewdmgetphysicaldevice"></a>[**WdfDeviceWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetphysicaldevice)  
检索 WDM 设备\_表示设备 PDO 的对象结构。 驱动程序可以在为设备创建框架设备对象之后调用此方法。

<a href="" id="wdfdevicewdmgetdeviceobject"></a>[**WdfDeviceWdmGetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)  
返回与指定框架设备对象相关联的 WDM 设备对象。

<a href="" id="wdfdevicewdmgetattacheddevice"></a>[**WdfDeviceWdmGetAttachedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetattacheddevice)  
返回[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)中下一个较低的 WDM 设备对象。

<a href="" id="wdfwdmdevicegetwdfdevicehandle"></a>[**WdfWdmDeviceGetWdfDeviceHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfwdmdevicegetwdfdevicehandle)  
返回与指定的 WDM 设备对象相关联的框架设备对象的句柄。

<a href="" id="wdfwdmdrivergetwdfdriverhandle"></a>[**WdfWdmDriverGetWdfDriverHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfwdmdrivergetwdfdriverhandle)  
返回与指定的 WDM 驱动程序对象相关联的 framework 驱动程序对象的句柄。

### <a name="obtaining-wdm-information-about-io-requests"></a>获取有关 i/o 请求的 WDM 信息

若要获取有关 i/o 请求的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfrequestwdmgetirp"></a>[**WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)  
返回与指定框架请求对象关联的 WDM [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构。 （另一方面，接收到框架外的 WDM IRP 的驱动程序可以通过调用[**WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)为 IRP 创建框架请求对象。）

<a href="" id="wdfrequestgetparameters"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
检索与指定框架请求对象关联的参数。 其中的大多数参数均来自请求的 WDM [i/o 堆栈位置](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)。）

<a href="" id="wdfrequestretrieveoutputwdmmdl"></a>[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)  
检索表示 i/o 请求的输出缓冲区的内存描述符列表（MDL）。

<a href="" id="wdfrequestretrieveinputwdmmdl"></a>[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)  
检索表示 i/o 请求输入缓冲区的 MDL。

<a href="" id="wdfrequestformatrequestusingcurrenttype"></a>[**WdfRequestFormatRequestUsingCurrentType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)  
将调用驱动程序的 i/o 堆栈位置的内容复制到驱动程序的本地 i/o 目标的 i/o 堆栈位置。

<a href="" id="wdfrequestwdmformatusingstacklocation"></a>[**WdfRequestWdmFormatUsingStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation)  
为驱动程序的本地 i/o 目标设置 i/o 堆栈位置的内容。

### <a name="obtaining-wdm-information-about-io-targets"></a>获取有关 i/o 目标的 WDM 信息

若要获取有关 i/o 目标的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfiotargetwdmgettargetdeviceobject"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
返回一个指针，该指针指向与本地或远程 i/o 目标相关联的 WDM 设备对象。

<a href="" id="wdfiotargetwdmgettargetfileobject"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
返回一个指针，该指针指向与远程 i/o 目标相关联[ **\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构的 WDM 文件。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
返回与远程 i/o 目标相关联的文件的句柄。

<a href="" id="wdfiotargetwdmgettargetphysicaldevice"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
返回一个指针，该指针指向表示远程 i/o 目标设备的 WDM 物理设备对象（PDO）。

### <a name="obtaining-wdm-information-about-interrupts-and-dpcs"></a>获取有关中断和 Dpc 的 WDM 信息

若要获取有关中断和延迟过程调用（Dpc）的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfinterruptwdmgetinterrupt"></a>[**WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)  
返回指向与指定框架中断对象相关联的 WDM [**KINTERRUPT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构的指针。

<a href="" id="wdfdpcwdmgetdpc"></a>[**WdfDpcWdmGetDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcwdmgetdpc)  
返回一个指向与指定框架 DPC 对象关联的 WDM [**KDPC**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构的指针。

### <a href="" id="obtaining-wdm-information-about-usb-i-o-targets"></a>获取有关 USB i/o 目标的 WDM 信息

若要获取有关 USB i/o 目标的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfusbtargetpipewdmgetpipehandle"></a>[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
返回与指定框架管道对象相关联的 USBD\_管道\_句柄类型的句柄。

### <a name="obtaining-wdm-information-about-the-registry"></a>获取有关注册表的 WDM 信息

若要获取有关注册表的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdfregistrywdmgethandle"></a>[**WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)  
返回框架注册表项对象表示的注册表项的 WDM 句柄。

### <a name="obtaining-wdm-information-about-file-objects"></a>获取有关文件对象的 WDM 信息

若要获取有关文件对象的 WDM 信息，驱动程序可以调用以下方法：

<a href="" id="wdffileobjectwdmgetfileobject"></a>[**WdfFileObjectWdmGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
返回与指定框架文件对象相关联[ **\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构的 WDM 文件。

 

 





