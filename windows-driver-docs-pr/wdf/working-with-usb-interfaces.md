---
title: 使用 USB 接口
description: 使用 USB 接口
ms.assetid: 6a1801e4-bd46-4a78-8c30-7dc62e41a37a
keywords:
- USB I/O 面向 WDK KMDF，USB 接口
- USB 接口 WDK KMDF
- framework 对象 WDK KMDF，USB 接口对象
- 接口对象 WDK KMDF
- 备用 USB 接口设置 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fca0e625f913dace801d250d4ae85d580edc0765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376882"
---
# <a name="working-with-usb-interfaces"></a>使用 USB 接口


框架表示为每个 USB 接口*framework USB 接口对象*。 当驱动程序[创建 framework USB 设备对象](working-with-usb-devices.md#creating-a-framework-usb-device-object)，框架将创建包含设备的第一个 USB 配置每个 USB 接口的 framework USB 接口对象。

大多数 USB 设备只有一个接口，并且此接口具有只有一个替代设置。 此类设备的驱动程序通常不需要使用框架的 USB 接口对象定义的对象方法。

如果您的驱动程序支持提供多个接口或替代设置的 USB 设备，接口对象方法启用驱动程序来执行以下操作：

-   [获取接口的信息。](#obtaining-interface-information)

-   [选择一项备用设置 USB 接口。](#selecting-an-alternate-setting-for-a-usb-interface)

### <a href="" id="obtaining-interface-information"></a> 获取接口的信息

您的驱动程序已调用后[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，它可以调用[ **WdfUsbTargetDeviceGetInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)到获取一个表示设备的 USB 接口之一的 framework USB 接口对象的句柄。 然后您的驱动程序可以调用 USB 接口对象定义的几种方法用于获取有关 USB 接口的信息。

您的驱动程序可以具有调用后随时调用以下方法[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters):

<a href="" id="---------wdfusbinterfacegetinterfacenumber--------"></a>[**WdfUsbInterfaceGetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)  
返回与 USB 接口对象相关联的 USB 接口号。

<a href="" id="---------wdfusbinterfacegetdescriptor--------"></a>[**WdfUsbInterfaceGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)  
检索与 USB 接口的替代设置之一相关联的 USB 接口描述符。

<a href="" id="---------wdfusbinterfacegetnumendpoints--------"></a>[**WdfUsbInterfaceGetNumEndpoints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumendpoints)  
返回与其中一个 USB 接口的替代设置相关联的终结点的数目。

<a href="" id="---------wdfusbinterfacegetendpointinformation--------"></a>[**WdfUsbInterfaceGetEndpointInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)  
检索有关终结点和其关联的管道信息。

您的驱动程序可以调用以下方法之后该维度被称为, [ **WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig):

<a href="" id="---------wdfusbinterfacegetconfiguredsettingindex--------"></a>[**WdfUsbInterfaceGetConfiguredSettingIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)  
返回标识为 USB 接口当前所选的备用设置的索引值。

<a href="" id="---------wdfusbinterfacegetnumconfiguredpipes--------"></a>[**WdfUsbInterfaceGetNumConfiguredPipes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)  
返回为指定的 USB 设备接口配置的管道数。

<a href="" id="---------wdfusbinterfacegetconfiguredpipe--------"></a>[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)  
返回与指定的 USB 设备接口和管道索引相关联的 framework 管道对象的句柄。

### <a href="" id="selecting-an-alternate-setting-for-a-usb-interface"></a> 选择一项备用设置为 USB 接口

驱动程序已调用后[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，该驱动程序可以调用[ **WdfUsbInterfaceGetNumSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings)以获取备用 USB 接口支持的设置的数量。

驱动程序已调用后[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)若要选择 USB 设备的配置，该驱动程序可以调用[ **WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)选择一项备用设置配置的 USB 接口之一。

从零开始的消息必须为连续编号在设备的备用设置。

有关相关信息，请参阅[如何在 USB 界面中选择一项备用设置](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)。

 

 





