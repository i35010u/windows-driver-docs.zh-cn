---
title: 在 UMDF 1.x 驱动程序中使用 USB 接口
description: 在 UMDF 1.x 驱动程序中使用 USB 接口
ms.assetid: fc25e3b2-1631-445e-9340-a8cc92c68733
keywords:
- UMDF WDK，USB 接口
- 用户模式驱动程序框架 WDK，USB 接口
- 用户模式驱动程序 WDK UMDF，USB 接口
- USB 接口 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837a1c1b7de9be46dca929cbf9119676c3eabb53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355914"
---
# <a name="working-with-usb-interfaces-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 接口


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架为框架 USB 接口对象表示每个 USB 接口。 当 UMDF 驱动程序创建 framework USB 设备对象时，框架将创建每个设备支持的 USB 接口的 framework USB 接口对象。

大多数 USB 设备只有一个接口，并且此接口具有只有一个备选设置。 此类设备的驱动程序通常不需要使用框架的 USB 接口对象定义的对象方法。

如果 UMDF 驱动程序支持提供多个接口或替代设置的 USB 设备，接口对象方法启用到驱动程序：

-   [获取接口的信息](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#obtaining-umdf-usb-interface-information)。

-   [选择一项备用设置 USB 接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#selecting-an-alternate-setting-for-a-umdf-usb-interface)。

### <a name="obtaining-umdf-usb-interface-information"></a>获取 UMDF USB 接口信息

后 UMDF 驱动程序已调用[ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)方法来创建 UMDF USB 目标设备对象，该驱动程序可以调用[ **IWDFUsbTargetDevice::GetNumInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)方法来获取设备支持的 USB 接口的数量。 接下来，驱动程序可以调用[ **IWDFUsbTargetDevice::RetrieveUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)方法来获取指向[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)接口公开USB 设备支持的接口。 然后该驱动程序可以调用每个 USB 接口对象定义的以下方法用于获取有关 USB 接口的信息：

<a href="" id="iwdfusbinterface--getinterfacenumber"></a>[**IWDFUsbInterface::GetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacenumber)  
获取与 USB 接口对象相关联的 USB 接口号。

<a href="" id="iwdfusbinterface--getinterfacedescriptor"></a>[**IWDFUsbInterface::GetInterfaceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)  
获取与 USB 接口的替代设置之一相关联的 USB 接口描述符。

<a href="" id="iwdfusbinterface--getnumendpoints"></a>[**IWDFUsbInterface::GetNumEndPoints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getnumendpoints)  
获取与一个 USB 接口的替代设置关联的终结点 （也称为管道） 的数目。

<a href="" id="iwdfusbinterface--getconfiguredsettingindex"></a>[**IWDFUsbInterface::GetConfiguredSettingIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)  
获取标识为 USB 接口当前所选的备用设置的索引值。

<a href="" id="iwdfusbinterface--retrieveusbpipeobject"></a>[**IWDFUsbInterface::RetrieveUsbPipeObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)  
检索一个指向[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)公开与指定的 USB 设备接口和管道索引相关联的 framework 管道对象的接口。

<a href="" id="iwdfusbinterface--getwinusbhandle"></a>[**IWDFUsbInterface::GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)  
获取与 USB 接口相关联的 WinUsb 接口句柄。

### <a name="selecting-an-alternate-setting-for-a-umdf-usb-interface"></a>选择一项备用设置 UMDF USB 接口

UMDF 驱动程序可以调用[ **IWDFUsbInterface::SelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)方法选择备用设置 USB 之一的接口的设备支持。

从零开始的消息必须为连续编号在设备的备用设置。

**重要**  选择某项设置使任何相关信息的接口和终结点。 因此，该驱动程序应获取此信息。 该驱动程序还必须放弃以前检索到任何 USB 管道对象，然后重新创建它们。

 

 

 





