---
title: PnP 和电源管理界面
description: PnP 和电源管理界面
keywords:
- 即插即用 WDK UMDF，电源管理接口
- PnP WDK UMDF，电源管理接口
- 电源管理 WDK UMDF，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b189c283ee0bfc6f815af4cd2c048e6b8c359e5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838713"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP 和电源管理界面


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当新设备到达系统时，框架将调用 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法以通知该到达的 UMDF 驱动程序，并在调用中传递 [**IWDFDriver**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 和 [**IWDFDeviceInitialize**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 接口。 驱动程序调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 方法为设备创建框架设备对象。

当驱动程序创建框架设备对象时，它们可以注册以下接口，以便框架通过调用与接口关联的方法来通知驱动程序-在即插即用 (PnP) 和电源管理 (PM) 事件发生时。

[**IPnpCallback**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallbackSelfManagedIo**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)

[**IPowerPolicyCallbackWakeFromS0**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

[**IPowerPolicyCallbackWakeFromSx**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

 

