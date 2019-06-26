---
title: 在 UMDF 1.x 驱动程序中使用 USB 设备
description: 在 UMDF 1.x 驱动程序中使用 USB 设备
ms.assetid: 144898a2-c4e1-495f-a6ca-72d9f09bda90
keywords:
- UMDF WDK、 USB 设备
- 用户模式驱动程序框架 WDK，USB 设备
- 用户模式驱动程序 WDK UMDF，USB 设备
- USB 设备 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b7b0bb17739bdb397d8c4c7f50f818aa426d0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383980"
---
# <a name="working-with-usb-devices-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 设备


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架为框架 USB 设备对象表示每个 USB 设备。 UMDF 驱动程序必须创建一个框架 USB 设备对象，该驱动程序才能访问对 USB I/O 目标框架的支持。 UMDF 提供了启用到 UMDF 驱动程序的 USB 设备对象方法：

-   [创建 UMDF USB 设备对象](#creating-a-umdf-usb-device-object)

-   [获取设备信息](#obtaining-umdf-usb-device-information)

-   [发送控制传输](#send-a-control-transfer-to-a-umdf-usb-device-object)

-   [设置电源策略](#set-power-policy-for-a-umdf-usb-device-object)

### <a name="creating-a-umdf-usb-device-object"></a>创建 UMDF USB 设备对象

若要使用框架的 USB I/O 目标功能，UMDF 驱动程序必须首先获取一个指向[IWDFUsbTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetfactory)接口。 若要获得指针，该驱动程序必须调用**QueryInterface**设备的方法[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)接口。 下面的代码示例演示如何调用**QueryInterface**获取指针：

```cpp
hr = pdevice->QueryInterface(IID_IWDFUsbTargetFactory, (LPVOID*)&ppUsbTargetFactory);
```

接下来必须调用该驱动程序[ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)方法来创建设备的 USB I/O 目标对象。 驱动程序将创建 USB I/O 目标后，该驱动程序可以将请求发送到 I/O 目标。 通常情况下，驱动程序调用**IWDFUsbTargetFactory::CreateUsbTargetDevice**内[ **IPnpCallbackHardware::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)回调函数。

驱动程序调用后**IWDFUsbTargetFactory::CreateUsbTargetDevice**，该驱动程序可以[获取 USB 设备信息](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices-in-umdf-1-x-drivers#obtaining-umdf-usb-device-information)（例如，USB 描述符的设备、 USB 接口和接口终结点）。 USB 描述符是 USB 规范中所述。

### <a name="obtaining-umdf-usb-device-information"></a>获取 UMDF USB 设备信息

UMDF 驱动程序调用后[ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)方法来创建 UMDF USB 目标设备对象，该驱动程序可以调用 USB 目标设备的以下方法对象定义用于获取有关 USB 设备的信息：

<a href="" id="iwdfusbtargetdevice--retrievedescriptor"></a>[**IWDFUsbTargetDevice::RetrieveDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)  
获取设备的 USB 设备描述符。

<a href="" id="iwdfusbtargetdevice--getnuminterfaces"></a>[**IWDFUsbTargetDevice::GetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)  
获取设备支持的 USB 接口的数量。

<a href="" id="iwdfusbtargetdevice--retrieveusbinterface"></a>[**IWDFUsbTargetDevice::RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)  
获取指向的指针[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)公开一个设备支持 USB 接口的接口。

<a href="" id="iwdfusbtargetdevice--retrievedeviceinformation"></a>[**IWDFUsbTargetDevice::RetrieveDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedeviceinformation)  
检索与 USB 设备相关联的功能信息。

<a href="" id="iwdfusbtargetdevice--retrievepowerpolicy"></a>[**IWDFUsbTargetDevice::RetrievePowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievepowerpolicy)  
检索 WinUsb 电源策略。

<a href="" id="iwdfusbtargetdevice--getwinusbhandle"></a>[**IWDFUsbTargetDevice::GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)  
获取与 I/O 目标设备对象相关联的 WinUsb 接口句柄。

### <a href="" id="send-a-control-transfer-to-a-umdf-usb-device-object"></a>将控件传输发送到 UMDF USB 设备对象

UMDF 驱动程序可以调用[ **IWDFUsbTargetDevice::FormatRequestForControlTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)方法来设置格式描述某一标准，设备类特定的 I/O 请求或特定于供应商的 USB控制传输。 然后，该驱动程序可以调用[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)方法以同步或异步发送请求。

### <a href="" id="set-power-policy-for-a-umdf-usb-device-object"></a>设置 UMDF USB 设备的电源策略

UMDF 驱动程序可以调用[ **IWDFUsbTargetDevice::SetPowerPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)方法以设置由 USB 设备 WinUsb 电源策略。 USB 设备的电源策略影响的更改到的设备的电源管理状态。

 

 





