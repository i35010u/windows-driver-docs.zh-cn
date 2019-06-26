---
title: PnP 和电源管理界面
description: PnP 和电源管理界面
ms.assetid: b80228f7-50be-4551-870b-2d7e2b5db239
keywords:
- 插 WDK UMDF，电源管理界面
- 即插即用 WDK UMDF，电源管理界面
- 电源管理 WDK UMDF，接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a43df368b6effbb89980b8a45872316713a62c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379661"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP 和电源管理界面


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当系统中，新设备到达时，框架将调用[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法以通知到达和传递的 UMDF 驱动程序[ **IWDFDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)并[ **IWDFDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)中调用的接口。 驱动程序调用[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法来创建该设备是 framework 的设备对象。

当驱动程序创建 framework 设备对象时，他们可以注册以下接口，以便该框架会通知驱动程序，通过调用与接口关联的方法 — 插即用 (PnP) 和电源管理 (PM) 事件发生时。

[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)

[**IPowerPolicyCallbackWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

[**IPowerPolicyCallbackWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

 

 





