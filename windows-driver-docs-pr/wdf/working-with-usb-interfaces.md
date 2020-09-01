---
title: 使用 USB 接口
description: 使用 USB 接口
ms.assetid: 6a1801e4-bd46-4a78-8c30-7dc62e41a37a
keywords:
- USB i/o 目标 WDK KMDF，USB 接口
- USB 接口 WDK KMDF
- framework 对象 WDK KMDF，USB 接口对象
- interface 对象 WDK KMDF
- 备用 USB 接口设置 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf1fa2090c3769fa2de8a9b49a94f49045ecb56
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185838"
---
# <a name="working-with-usb-interfaces"></a>使用 USB 接口


框架将每个 USB 接口表示为 *框架 USB 接口对象*。 当驱动程序 [创建框架 usb 设备对象](working-with-usb-devices.md#creating-a-framework-usb-device-object)时，框架会为设备的第一个 usb 配置包含的每个 usb 接口创建一个框架 usb 接口对象。

大多数 USB 设备只有一个接口，接口只有一个备用设置。 此类设备的驱动程序通常不需要使用框架的 USB 接口对象所定义的对象方法。

如果驱动程序支持提供多个接口或备用设置的 USB 设备，则 interface 对象方法使驱动程序能够执行以下操作：

-   [获取接口信息。](#obtaining-interface-information)

-   [选择 USB 接口的替代设置。](#selecting-an-alternate-setting-for-a-usb-interface)

### <a name="obtaining-interface-information"></a><a href="" id="obtaining-interface-information"></a> 获取接口信息

当你的驱动程序调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)后，它可以调用 [**WdfUsbTargetDeviceGetInterface**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface) 来获取框架 usb 接口对象的句柄，该对象表示设备的一个 usb 接口。 然后，驱动程序可以调用 USB 接口对象定义的几种方法来获取有关 USB 接口的信息。

驱动程序可以在调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)后随时调用以下方法：

<a href="" id="---------wdfusbinterfacegetinterfacenumber--------"></a>[**WdfUsbInterfaceGetInterfaceNumber**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)  
返回与 USB 接口对象关联的 USB 接口号。

<a href="" id="---------wdfusbinterfacegetdescriptor--------"></a>[**WdfUsbInterfaceGetDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)  
检索与 USB 接口的备用设置之一关联的 USB 接口描述符。

<a href="" id="---------wdfusbinterfacegetnumendpoints--------"></a>[**WdfUsbInterfaceGetNumEndpoints**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumendpoints)  
返回与 USB 接口的备用设置之一关联的终结点的数目。

<a href="" id="---------wdfusbinterfacegetendpointinformation--------"></a>[**WdfUsbInterfaceGetEndpointInformation**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)  
检索有关终结点及其关联管道的信息。

在调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)之后，你的驱动程序可以调用以下方法：

<a href="" id="---------wdfusbinterfacegetconfiguredsettingindex--------"></a>[**WdfUsbInterfaceGetConfiguredSettingIndex**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)  
返回一个索引值，该值标识当前为 USB 接口选择的备用设置。

<a href="" id="---------wdfusbinterfacegetnumconfiguredpipes--------"></a>[**WdfUsbInterfaceGetNumConfiguredPipes**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)  
返回为指定 USB 设备接口配置的管道的数目。

<a href="" id="---------wdfusbinterfacegetconfiguredpipe--------"></a>[**WdfUsbInterfaceGetConfiguredPipe**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)  
返回与指定的 USB 设备接口和管道索引相关联的框架管道对象的句柄。

### <a name="selecting-an-alternate-setting-for-a-usb-interface"></a><a href="" id="selecting-an-alternate-setting-for-a-usb-interface"></a> 选择 USB 接口的替代设置

驱动程序调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)后，该驱动程序可以调用 [**WDFUSBINTERFACEGETNUMSETTINGS**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings) 来获取 USB 接口支持的备用设置的数目。

在驱动程序调用 [**WdfUsbTargetDeviceSelectConfig**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) 以选择某个 usb 设备的配置后，该驱动程序可以调用 [**WdfUsbInterfaceSelectSetting**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) 为配置的一个 usb 接口选择备用设置。

设备的备用设置必须连续编号（从零开始）。

有关相关信息，请参阅 [如何在 USB 接口中选择替代设置](../usbcon/index.md)。

 

