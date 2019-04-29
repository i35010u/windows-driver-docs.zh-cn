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
ms.openlocfilehash: 738e982145d760505882610f00f605f45db24f4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383536"
---
# <a name="working-with-usb-interfaces"></a>使用 USB 接口


框架表示为每个 USB 接口*framework USB 接口对象*。 当驱动程序[创建 framework USB 设备对象](working-with-usb-devices.md#creating-a-framework-usb-device-object)，框架将创建包含设备的第一个 USB 配置每个 USB 接口的 framework USB 接口对象。

大多数 USB 设备只有一个接口，并且此接口具有只有一个替代设置。 此类设备的驱动程序通常不需要使用框架的 USB 接口对象定义的对象方法。

如果您的驱动程序支持提供多个接口或替代设置的 USB 设备，接口对象方法启用驱动程序来执行以下操作：

-   [获取接口的信息。](#obtaining-interface-information)

-   [选择一项备用设置 USB 接口。](#selecting-an-alternate-setting-for-a-usb-interface)

### <a href="" id="obtaining-interface-information"></a> 获取接口的信息

您的驱动程序已调用后[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)，它可以调用[ **WdfUsbTargetDeviceGetInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550092)到获取一个表示设备的 USB 接口之一的 framework USB 接口对象的句柄。 然后您的驱动程序可以调用 USB 接口对象定义的几种方法用于获取有关 USB 接口的信息。

您的驱动程序可以具有调用后随时调用以下方法[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428):

<a href="" id="---------wdfusbinterfacegetinterfacenumber--------"></a>[**WdfUsbInterfaceGetInterfaceNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550065)  
返回与 USB 接口对象相关联的 USB 接口号。

<a href="" id="---------wdfusbinterfacegetdescriptor--------"></a>[**WdfUsbInterfaceGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550060)  
检索与 USB 接口的替代设置之一相关联的 USB 接口描述符。

<a href="" id="---------wdfusbinterfacegetnumendpoints--------"></a>[**WdfUsbInterfaceGetNumEndpoints**](https://msdn.microsoft.com/library/windows/hardware/ff550068)  
返回与其中一个 USB 接口的替代设置相关联的终结点的数目。

<a href="" id="---------wdfusbinterfacegetendpointinformation--------"></a>[**WdfUsbInterfaceGetEndpointInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550063)  
检索有关终结点和其关联的管道信息。

您的驱动程序可以调用以下方法之后该维度被称为, [ **WdfUsbTargetDeviceSelectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff550101):

<a href="" id="---------wdfusbinterfacegetconfiguredsettingindex--------"></a>[**WdfUsbInterfaceGetConfiguredSettingIndex**](https://msdn.microsoft.com/library/windows/hardware/ff550059)  
返回标识为 USB 接口当前所选的备用设置的索引值。

<a href="" id="---------wdfusbinterfacegetnumconfiguredpipes--------"></a>[**WdfUsbInterfaceGetNumConfiguredPipes**](https://msdn.microsoft.com/library/windows/hardware/ff550066)  
返回为指定的 USB 设备接口配置的管道数。

<a href="" id="---------wdfusbinterfacegetconfiguredpipe--------"></a>[**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)  
返回与指定的 USB 设备接口和管道索引相关联的 framework 管道对象的句柄。

### <a href="" id="selecting-an-alternate-setting-for-a-usb-interface"></a> 选择一项备用设置为 USB 接口

驱动程序已调用后[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)，该驱动程序可以调用[ **WdfUsbInterfaceGetNumSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff550070)以获取备用 USB 接口支持的设置的数量。

驱动程序已调用后[ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)若要选择 USB 设备的配置，该驱动程序可以调用[ **WdfUsbInterfaceSelectSetting**](https://msdn.microsoft.com/library/windows/hardware/ff550073)选择一项备用设置配置的 USB 接口之一。

从零开始的消息必须为连续编号在设备的备用设置。

有关相关信息，请参阅[如何在 USB 界面中选择一项备用设置](https://msdn.microsoft.com/library/windows/hardware/hh968309)。

 

 





