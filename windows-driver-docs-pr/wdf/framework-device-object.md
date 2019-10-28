---
title: 框架设备对象
description: 框架设备对象
ms.assetid: 6be47eac-d6e4-43d1-bf2d-d49dcb2273c0
keywords:
- UMDF 对象 WDK，设备对象
- framework 对象 WDK UMDF，设备对象
- 设备对象 WDK UMDF
- IWDFDevice
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0008ec6cc16be804627815954684d443a7faeb35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843184"
---
# <a name="framework-device-object"></a>框架设备对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

通过[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口向驱动程序公开框架设备对象。 框架设备对象是系统上的设备的框架表示形式。 每个设备对象都有一个父驱动程序对象。

当新设备到达系统时，框架将调用[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法来通知到达的驱动程序，并在调用中传递[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)和[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)接口。 驱动程序可以调用 IWDFDeviceInitialize 接口的方法来初始化新设备。 例如，驱动程序将调用[**IWDFDeviceInitialize：： RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)方法来查询在设备安装过程中提供的设备信息。 然后，该驱动程序可以调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法来配置和创建设备对象。

当驱动程序创建框架设备对象时，它们可以注册其[IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)、 [IPnpCallbackSelfManagedIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)、 [IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)、 [IFileCallbackCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ifilecallbackcleanup)和[IFileCallbackClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ifilecallbackclose)接口。 然后，框架将在文件清理和关闭并即插即用（PnP）和电源管理（PM）事件发生时通知驱动程序。 有关支持 PnP 和 PM 的详细信息，请参阅[基于 UMDF 的驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

 

 





