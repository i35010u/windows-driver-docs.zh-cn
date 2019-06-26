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
ms.openlocfilehash: d8239134e16f2ac2d7ed0f2ec31ed225d0592785
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368681"
---
# <a name="framework-device-object"></a>框架设备对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework 设备对象公开到由驱动程序[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)接口。 Framework 设备对象是在系统上设备的 framework 表示形式。 每个设备对象具有父驱动程序对象。

当系统中，新设备到达时，框架将调用[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法以通知到达和传递的驱动程序[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)和[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)中调用的接口。 该驱动程序可以调用 IWDFDeviceInitialize 接口来初始化新的设备的方法。 例如，驱动程序调用[ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)方法来查询有关设备安装的一部分提供的设备信息。 然后，该驱动程序可以调用[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法配置并创建设备对象。

当驱动程序创建 framework 设备对象时，它们可以将其[IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)， [IPnpCallbackSelfManagedIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)， [IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)， [IFileCallbackCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ifilecallbackcleanup)，并[IFileCallbackClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ifilecallbackclose)接口。 清除和关闭的文件和插 (PnP) 和电源管理 (PM) 事件发生时，框架然后会通知驱动程序。 有关支持即插即用和 PM 的详细信息，请参阅[基于 UMDF 驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

 

 





