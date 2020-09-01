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
ms.openlocfilehash: 7374fdf938601a13b5265da20cfef74a9b1788cd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185847"
---
# <a name="working-with-usb-interfaces-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 接口


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架将每个 USB 接口表示为框架 USB 接口对象。 当 UMDF 驱动程序创建框架 USB 设备对象时，框架会为设备支持的每个 USB 接口创建一个框架 USB 接口对象。

大多数 USB 设备只有一个接口，接口只有一个替代设置。 此类设备的驱动程序通常不需要使用框架的 USB 接口对象所定义的对象方法。

如果 UMDF 驱动程序支持提供多个接口或备用设置的 USB 设备，则 interface 对象方法使驱动程序能够：

-   [获取接口信息](#obtaining-umdf-usb-interface-information)。

-   [选择 USB 接口的替代设置](#selecting-an-alternate-setting-for-a-umdf-usb-interface)。

### <a name="obtaining-umdf-usb-interface-information"></a>获取 UMDF-USB 接口信息

在 UMDF 驱动程序调用 [**IWDFUsbTargetFactory：： CreateUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice) 方法来创建一个 UMDF USB 目标设备对象之后，该驱动程序可以调用 [**IWDFUsbTargetDevice：： GetNumInterfaces**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces) 方法来获取设备支持的 USB 接口数量。 接下来，驱动程序可以调用 [**IWDFUsbTargetDevice：： RetrieveUsbInterface**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface) 方法来获取指向 [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface) 接口的指针，该接口公开设备支持的 USB 接口。 然后，驱动程序可以调用以下方法，每个 USB 接口对象定义这些方法来获取有关 USB 接口的信息：

<a href="" id="iwdfusbinterface--getinterfacenumber"></a>[**IWDFUsbInterface::GetInterfaceNumber**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacenumber)  
获取与 USB 接口对象关联的 USB 接口号。

<a href="" id="iwdfusbinterface--getinterfacedescriptor"></a>[**IWDFUsbInterface::GetInterfaceDescriptor**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)  
获取与 USB 接口的备用设置之一关联的 USB 接口描述符。

<a href="" id="iwdfusbinterface--getnumendpoints"></a>[**IWDFUsbInterface::GetNumEndPoints**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getnumendpoints)  
获取 (也称为管道) 的终结点数目，这些终结点与 USB 接口的备用设置之一相关联。

<a href="" id="iwdfusbinterface--getconfiguredsettingindex"></a>[**IWDFUsbInterface::GetConfiguredSettingIndex**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)  
获取一个索引值，该值标识当前为 USB 接口选择的备用设置。

<a href="" id="iwdfusbinterface--retrieveusbpipeobject"></a>[**IWDFUsbInterface::RetrieveUsbPipeObject**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)  
检索指向 [IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) 接口的指针，该接口公开与指定的 USB 设备接口和管道索引相关联的框架管道对象。

<a href="" id="iwdfusbinterface--getwinusbhandle"></a>[**IWDFUsbInterface::GetWinUsbHandle**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)  
获取与 USB 接口相关联的 WinUsb 接口句柄。

### <a name="selecting-an-alternate-setting-for-a-umdf-usb-interface"></a>为 UMDF USB 接口选择备用设置

UMDF 驱动程序可以调用 [**IWDFUsbInterface：： SelectSetting**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting) 方法为设备支持的某个 USB 接口选择备用设置。

设备的备用设置必须连续编号（从零开始）。

**重要提示**   选择某个设置会使有关该接口和终结点的任何信息失效。 因此，该驱动程序应再次获取此信息。 驱动程序还必须丢弃先前检索的任何 USB 管道对象并重新创建它们。

 

 

