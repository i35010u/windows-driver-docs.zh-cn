---
title: 使用 USB 设备
description: 本主题介绍从版本2开始 Kernel-Mode Driver Framework (KMDF) 或 User-Mode Driver Framework (UMDF) 驱动程序的操作可以使用 Windows 驱动程序框架所提供的 USB 设备对象方法 (WDF) 来执行。
keywords:
- USB i/o 目标 WDK KMDF，framework USB 设备对象
- framework 对象 WDK KMDF，USB 设备对象
- USB 请求块 WDK KMDF
- URBs WDK KMDF
- USB i/o 目标 WDK KMDF，USB 设备
- 控件传输 WDK KMDF
- 重启端口 WDK KMDF
- 重置端口 WDK KMDF
- 发送 URBs WDK KMDF
- Unicode 字符串 WDK KMDF
- 状态信息 WDK KMDF，USB i/o 目标
- 设备对象 WDK KMDF
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2c1beba76ffecb702c21ee572a1f545ba89b9054
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124251"
---
# <a name="working-with-usb-devices"></a>使用 USB 设备


本主题介绍从版本2开始 Kernel-Mode Driver Framework (KMDF) 或 User-Mode Driver Framework (UMDF) 驱动程序的操作可以使用 Windows 驱动程序框架所提供的 USB 设备对象方法 (WDF) 来执行。

它包含以下部分：

-   [创建 USB 设备对象](#creating-a-framework-usb-device-object)
-   [配置 USB 设备](#selecting-a-device-configuration)
-   [获取设备信息](#obtaining-device-information)
-   [获取 USB 描述符](#obtaining-a-device-s-unicode-strings)
-   [发送控件传输](#sending-a-control-transfer)
-   [重置并 Power-Cycling 设备端口](#resetting-and-power-cycling-a-device-s-port)
-   [将 URB 发送到设备](#sending-a-urb-to-a-device)

有关编写简单的基于 KMDF 的 USB 客户端驱动程序的分步说明，请参阅 [如何编写第一个 usb 客户端驱动程序 (KMDF) ](/windows-hardware/drivers/ddi/index)。

## <a name="creating-a-usb-device-object"></a><a href="" id="creating-a-framework-usb-device-object"></a> 创建 USB 设备对象


若要使用框架的 USB i/o 目标对象 (WDFUSBDEVICE、WDFUSBINTERFACE 和 WDFUSBPIPE) ，你的客户端驱动程序必须先调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) ，才能创建 USB 设备对象。 通常，驱动程序从其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数调用 **WdfUsbTargetDeviceCreateWithParameters** 。

当驱动程序调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)时，框架会创建一个 WDFUSBDEVICE 对象，并将其与表示该 USB 设备的 FDO 相关联。 方法返回新的框架 USB 设备对象的句柄，USB 客户端驱动程序可使用该对象与物理设备通信。

调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)之后，驱动程序可以调用 [**WdfUsbTargetDeviceGetDeviceDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor) 和 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor) 从设备获取 USB 描述符。 这些描述符包含有关设备的第一个配置、其接口设置及其定义的终结点的信息。  (在官方 USB 规范中定义 USB 描述符 ) 

## <a name="configuring-a-usb-device"></a><a href="" id="selecting-a-device-configuration"></a>配置 USB 设备


[**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法还会为设备的第一个配置所包含的每个 USB 接口创建一个框架 usb 接口对象。

调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)之后，客户端驱动程序必须调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) 来选择配置。 此方法为所选配置中接口的每个替代设置创建框架接口对象。

方法还会创建管道对象，这些对象表示在所选配置的每个接口的每个替代设置中定义的终结点。

选择配置后，如果需要，可以更改配置接口的 [备用设置](working-with-usb-interfaces.md#selecting-an-alternate-setting-for-a-usb-interface) 。

你还可以调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) 来 deconfigure 设备。

如需相关信息，请参阅：

-   [如何选择 USB 设备的配置](../usbcon/how-to-select-a-configuration-for-a-usb-device.md)
-   [如何在 USB 界面中选择备用设置](../usbcon/index.md)

## <a name="obtaining-device-information"></a><a href="" id="obtaining-device-information"></a> 获取设备信息


配置设备后，客户端驱动程序可以调用以下方法来获取有关 USB 设备的信息：

<a href="" id="wdfusbtargetdevicequeryusbcapability"></a>[**WdfUsbTargetDeviceQueryUsbCapability**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)  
确定主机控制器和 USB 驱动程序堆栈是否支持特定功能。 在调用 [**WdfUsbTargetDeviceQueryUsbCapability**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)之前，驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="wdfusbtargetdevicegetiotarget"></a>[**WdfUsbTargetDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)  
返回与 USB 设备关联的 i/o 目标对象的句柄。 驱动程序可以将此句柄传递给 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 或 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)。

<a href="" id="wdfusbtargetdeviceretrieveinformation"></a>[**WdfUsbTargetDeviceRetrieveInformation**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)  
检索与 USB 设备关联的版本和功能信息。

<a href="" id="wdfusbtargetdeviceisconnectedsynchronous--kmdf-only-"></a>[**WdfUsbTargetDeviceIsConnectedSynchronous (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous)  
确定设备是否已连接。

<a href="" id="wdfusbtargetdeviceretrievecurrentframenumber--kmdf-only-"></a>[**WdfUsbTargetDeviceRetrieveCurrentFrameNumber (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrievecurrentframenumber)  
检索当前的 USB 帧号。

## <a name="getting-usb-descriptors"></a><a href="" id="obtaining-a-device-s-unicode-strings"></a>获取 USB 描述符


若要获取 USB 设备描述符中包含的 Unicode 字符串，驱动程序可以调用以下任一方法：

<a href="" id="wdfusbtargetdevicegetdevicedescriptor"></a>[**WdfUsbTargetDeviceGetDeviceDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)  
获取设备的 [USB 设备描述符](/windows-hardware/drivers/ddi/index)。

<a href="" id="wdfusbtargetdeviceretrieveconfigdescriptor"></a>[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)  
获取设备的 [USB 配置描述符](/windows-hardware/drivers/ddi/index)、接口描述符和终结点说明符。

<a href="" id="---------wdfusbtargetdevicequerystring--------"></a>[**WdfUsbTargetDeviceQueryString**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequerystring)  
将 Unicode 字符串复制到驱动程序提供的缓冲区。

<a href="" id="---------wdfusbtargetdeviceallocandquerystring--------"></a>[**WdfUsbTargetDeviceAllocAndQueryString**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceallocandquerystring)  
将 Unicode 字符串复制到框架提供的缓冲区。

<a href="" id="---------wdfusbtargetdeviceformatrequestforstring--------"></a>[**WdfUsbTargetDeviceFormatRequestForString**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforstring)  
格式化 Unicode 字符串的请求。 驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 来同步或异步发送请求。

## <a name="sending-a-control-transfer"></a><a href="" id="sending-a-control-transfer"></a> 发送控件传输


驱动程序可以调用以下方法发送 i/o 请求，这些请求描述了标准的设备特定于设备或特定于供应商的 USB 控制传输。

<a href="" id="---------wdfusbtargetdevicesendcontroltransfersynchronously--------"></a>[**WdfUsbTargetDeviceSendControlTransferSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)  
同步发送 USB 控件传输请求。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcontroltransfer--------"></a>[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)  
格式化 USB 控件传输请求。 驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 来同步或异步发送请求。

有关相关信息，请参阅 [如何发送 USB 控件传输](/windows-hardware/drivers/ddi/index)。

## <a name="resetting-and-power-cycling-a-devices-port"></a><a href="" id="resetting-and-power-cycling-a-device-s-port"></a> 重置并 Power-Cycling 设备端口


你的驱动程序可以调用以下方法来重置或重启设备连接到的 USB 端口：

<a href="" id="---------wdfusbtargetdeviceresetportsynchronously"></a>[**WdfUsbTargetDeviceResetPortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)  
同步发送用于重置设备 USB 端口的请求。

<a href="" id="---------wdfusbtargetdevicecycleportsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceCyclePortSynchronously (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously)  
以同步方式将请求发送到设备的 USB 端口。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcycleport--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForCyclePort (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport)  
格式化请求以对设备的 USB 端口进行电源重启。 驱动程序必须调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 以同步或异步发送请求。

有关相关信息，请参阅 [如何从 USB 管道中恢复错误](../usbcon/index.md)。

## <a name="sending-an-urb-to-a-device"></a><a href="" id="sending-a-urb-to-a-device"></a> 将 URB 发送到设备


如果 KMDF 驱动程序通过发送 i/o 请求（其中包含 URBs）与 USB 设备通信，则驱动程序可以调用以下方法：

<a href="" id="wdfusbtargetdevicecreateurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateUrb (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)  
 (URB) 分配 USB 请求块。 在调用 [**WdfUsbTargetDeviceCreateUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)之前，驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="wdfusbtargetdevicecreateisochurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateIsochUrb (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)  
分配 (URB) 的同步 USB 请求块。 在调用 [**WdfUsbTargetDeviceCreateIsochUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)之前，驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)。

<a href="" id="---------wdfusbtargetdevicesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceSendUrbSynchronously (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)  
同步发送包含 URB 的 i/o 请求。

<a href="" id="---------wdfusbtargetdeviceformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForUrb (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)  
设置包含 URB 的 i/o 请求的格式。 驱动程序必须调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 以同步或异步发送请求。

<a href="" id="---------wdfusbtargetdevicewdmgetconfigurationhandle--kmdf-only-"></a>[**WdfUsbTargetDeviceWdmGetConfigurationHandle (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)  
返回设备的 USBD 配置句柄。 一些 URBs 需要此句柄。

有关 URBs 的一般概念背景，请参阅 [分配和生成 URBs](../usbcon/how-to-add-xrb-support-for-client-drivers.md)。

