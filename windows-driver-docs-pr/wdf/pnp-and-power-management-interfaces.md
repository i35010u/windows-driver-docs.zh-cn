---
title: PnP 和电源管理界面
description: PnP 和电源管理界面
ms.assetid: b80228f7-50be-4551-870b-2d7e2b5db239
keywords:
- 即插即用 WDK UMDF，电源管理接口
- PnP WDK UMDF，电源管理接口
- 电源管理 WDK UMDF，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c745f7aa5da3d775df67c1d56be465d786f78bcc
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210873"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP 和电源管理界面


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当新设备到达系统时，框架将调用[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法以通知该到达的 UMDF 驱动程序，并在调用中传递[**IWDFDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)和[**IWDFDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)接口。 驱动程序调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法为设备创建框架设备对象。

当驱动程序创建框架设备对象时，它们可以注册以下接口，以便框架通过调用与接口关联的方法（在即插即用（PnP）和电源管理（PM）事件发生时）来通知驱动程序。

[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)

[**IPowerPolicyCallbackWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

[**IPowerPolicyCallbackWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

 

 





