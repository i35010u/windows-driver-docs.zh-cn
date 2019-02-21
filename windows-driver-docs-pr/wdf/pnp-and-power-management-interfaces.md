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
ms.openlocfilehash: d2b71c6c4d38d33d7a0381cc0244b9199731270b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547340"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP 和电源管理界面


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当系统中，新设备到达时，框架将调用[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法以通知到达和传递的 UMDF 驱动程序[ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893)并[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)中调用的接口。 驱动程序调用[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法来创建该设备是 framework 的设备对象。

当驱动程序创建 framework 设备对象时，他们可以注册以下接口，以便该框架会通知驱动程序，通过调用与接口关联的方法 — 插即用 (PnP) 和电源管理 (PM) 事件发生时。

[**IPnpCallback**](https://msdn.microsoft.com/library/windows/hardware/ff556762)

[**IPnpCallbackSelfManagedIo**](https://msdn.microsoft.com/library/windows/hardware/ff556776)

[**IPnpCallbackHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764)

[**IPowerPolicyCallbackWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff556815)

[**IPowerPolicyCallbackWakeFromSx**](https://msdn.microsoft.com/library/windows/hardware/ff556825)

 

 





