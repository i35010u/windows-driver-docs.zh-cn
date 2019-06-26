---
title: 使用 USB 设备
description: 本主题描述在版本 2 中启动的内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序可以使用提供的 Windows 驱动程序框架 (WDF) 的 USB 设备对象方法执行的操作。
ms.assetid: 8e06f3c4-1a58-4b9f-ae89-ff4e37eb8f0a
keywords:
- USB I/O 面向 WDK KMDF，framework USB 设备对象
- framework 对象 WDK KMDF，USB 设备对象
- USB 请求阻止 WDK KMDF
- URBs WDK KMDF
- USB I/O 面向 WDK KMDF，USB 设备
- 控制传输 WDK KMDF
- 关闭再打开端口 WDK KMDF
- 重置端口 WDK KMDF
- 发送 URBs WDK KMDF
- Unicode 字符串 WDK KMDF
- WDK KMDF，USB I/O 目标的状态信息
- 设备对象 WDK KMDF
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: b1f8fc8c1b7554856ad2f2deca51eb487cacedb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355910"
---
# <a name="working-with-usb-devices"></a>使用 USB 设备


本主题描述在版本 2 中启动的内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序可以使用提供的 Windows 驱动程序框架 (WDF) 的 USB 设备对象方法执行的操作。

它包含以下各节：

-   [创建的 USB 设备对象](#creating-a-framework-usb-device-object)
-   [配置 USB 设备](#selecting-a-device-configuration)
-   [获取设备信息](#obtaining-device-information)
-   [获取 USB 描述符](#obtaining-a-device-s-unicode-strings)
-   [发送控制传输](#sending-a-control-transfer)
-   [重置和关闭再打开设备的端口](#resetting-and-power-cycling-a-device-s-port)
-   [向设备发送 URB](#sending-a-urb-to-a-device)

有关编写简单的基于 KMDF 的 USB 客户端驱动程序的分步说明，请参阅[如何编写第一个 USB 客户端驱动程序 (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

## <a href="" id="creating-a-framework-usb-device-object"></a> 创建的 USB 设备对象


若要使用框架的 USB I/O 目标对象 （WDFUSBDEVICE、 WDFUSBINTERFACE 和 WDFUSBPIPE），客户端驱动程序必须首先调用[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)创建 USB 设备对象。 通常情况下，驱动程序调用**WdfUsbTargetDeviceCreateWithParameters**从其[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数。

当驱动程序调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，框架将创建 WDFUSBDEVICE 对象并将其与表示 USB 设备 FDO 关联。 该方法返回的句柄 USB 客户端驱动程序然后可以使用与物理设备进行通信的新框架 USB 设备对象。

在调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，该驱动程序可以调用[ **WdfUsbTargetDeviceGetDeviceDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)并[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)从设备获取 USB 描述符。 这些描述符包含有关设备的第一个配置、 其接口设置，以及其定义的终结点的信息。 （USB 描述符规范中定义官方 USB。）

## <a href="" id="selecting-a-device-configuration"></a>配置 USB 设备


[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法还会创建设备的第一个配置包含每个 USB 接口的 framework USB 接口对象。

在调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，客户端驱动程序必须调用[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)若要选择的配置。 此方法中所选的配置创建框架接口对象的接口的每个备选设置。

该方法还会创建管道对象表示在所选配置的每个接口的每个备用设置中定义的终结点。

选择一种配置后，你可以[更改替代设置](working-with-usb-interfaces.md#selecting-an-alternate-setting-for-a-usb-interface)对于配置的接口，如有必要。

您还可以调用[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)若要取消配置设备。

有关相关信息，请参阅：

-   [如何选择 USB 设备的配置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [如何在 USB 界面中选择一项备用设置](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

## <a href="" id="obtaining-device-information"></a> 获取设备信息


配置设备之后, 您的客户端驱动程序可以调用以下方法来获取有关 USB 设备的信息：

<a href="" id="wdfusbtargetdevicequeryusbcapability"></a>[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)  
确定主控制器和 USB 驱动程序堆栈是否支持某项特定功能。 然后再调用[ **WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)，驱动程序必须调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="wdfusbtargetdevicegetiotarget"></a>[**WdfUsbTargetDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)  
返回的句柄与 USB 设备相关联的 I/O 目标对象。 该驱动程序可以将传递到此句柄[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)或[ **WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)。

<a href="" id="wdfusbtargetdeviceretrieveinformation"></a>[**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)  
检索与 USB 设备相关联的版本和功能的信息。

<a href="" id="wdfusbtargetdeviceisconnectedsynchronous--kmdf-only-"></a>[**WdfUsbTargetDeviceIsConnectedSynchronous (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous)  
确定是否已连接设备。

<a href="" id="wdfusbtargetdeviceretrievecurrentframenumber--kmdf-only-"></a>[**WdfUsbTargetDeviceRetrieveCurrentFrameNumber (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrievecurrentframenumber)  
检索当前的 USB 帧数。

## <a href="" id="obtaining-a-device-s-unicode-strings"></a>获取 USB 描述符


若要获取包含在 USB 设备的描述符中的 Unicode 字符串，该驱动程序可以调用任意以下方法：

<a href="" id="wdfusbtargetdevicegetdevicedescriptor"></a>[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)  
获取设备的[USB 设备描述符](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

<a href="" id="wdfusbtargetdeviceretrieveconfigdescriptor"></a>[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)  
获取设备的[USB 配置描述符](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，接口描述符和终结点描述符。

<a href="" id="---------wdfusbtargetdevicequerystring--------"></a>[**WdfUsbTargetDeviceQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequerystring)  
将 Unicode 字符串复制到驱动程序所提供的缓冲区。

<a href="" id="---------wdfusbtargetdeviceallocandquerystring--------"></a>[**WdfUsbTargetDeviceAllocAndQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceallocandquerystring)  
将 Unicode 字符串复制到框架提供的缓冲区。

<a href="" id="---------wdfusbtargetdeviceformatrequestforstring--------"></a>[**WdfUsbTargetDeviceFormatRequestForString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforstring)  
设置格式的 Unicode 字符串的请求。 该驱动程序可以调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)以同步或异步发送请求。

## <a href="" id="sending-a-control-transfer"></a> 发送控制传输


您的驱动程序可以调用以下方法来发送 I/O 请求，用于描述某一标准，特定于设备类的或特定于供应商的 USB 控制传输。

<a href="" id="---------wdfusbtargetdevicesendcontroltransfersynchronously--------"></a>[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)  
以同步方式发送的 USB 控制传输请求。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcontroltransfer--------"></a>[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)  
设置请求的 USB 控制传输格式。 该驱动程序可以调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)以同步或异步发送请求。

有关相关信息，请参阅[如何发送 USB 控制传输](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

## <a href="" id="resetting-and-power-cycling-a-device-s-port"></a> 重置和关闭再打开设备的端口


您的驱动程序可以调用以下方法来重置或重新启动的设备连接到的 USB 端口：

<a href="" id="---------wdfusbtargetdeviceresetportsynchronously"></a>[**WdfUsbTargetDeviceResetPortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)  
以同步方式发送请求以重置设备的 USB 端口。

<a href="" id="---------wdfusbtargetdevicecycleportsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceCyclePortSynchronously (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously)  
以同步方式发送请求以重启设备的 USB 端口。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcycleport--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForCyclePort (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport)  
设置格式的请求来重新启动设备的 USB 端口。 该驱动程序必须调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)以同步或异步发送请求。

有关相关信息，请参阅[如何从 USB 管道错误中恢复](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)。

## <a href="" id="sending-a-urb-to-a-device"></a> 向设备发送 URB


如果 KMDF 驱动程序通过发送包含 URBs 的 I/O 请求具有其 USB 设备进行通信，该驱动程序可以调用以下方法：

<a href="" id="wdfusbtargetdevicecreateurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateUrb (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)  
分配 USB 请求块 (URB)。 然后再调用[ **WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)，驱动程序必须调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="wdfusbtargetdevicecreateisochurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateIsochUrb (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)  
分配等时的 USB 请求块 (URB)。 然后再调用[ **WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)，驱动程序必须调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="---------wdfusbtargetdevicesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceSendUrbSynchronously (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)  
以同步方式将发送包含 URB 的 I/O 请求。

<a href="" id="---------wdfusbtargetdeviceformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForUrb (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)  
设置包含 URB 的 I/O 请求的格式。 该驱动程序必须调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)以同步或异步发送请求。

<a href="" id="---------wdfusbtargetdevicewdmgetconfigurationhandle--kmdf-only-"></a>[**WdfUsbTargetDeviceWdmGetConfigurationHandle (仅适用于 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)  
返回设备的 USBD 配置句柄。 某些 URBs 要求此句柄。

URBs 的一般概念背景，请参阅[Allocating 和构建 URBs](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-add-xrb-support-for-client-drivers)。

 

 





