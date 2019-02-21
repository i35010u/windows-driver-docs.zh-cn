---
title: Framework 设备对象
description: Framework 设备对象
ms.assetid: 6be47eac-d6e4-43d1-bf2d-d49dcb2273c0
keywords:
- UMDF 对象 WDK，设备对象
- framework 对象 WDK UMDF，设备对象
- 设备对象 WDK UMDF
- IWDFDevice
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f8e44cd23797d37b77232f3282970820edb3c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520493"
---
# <a name="framework-device-object"></a>Framework 设备对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework 设备对象公开到由驱动程序[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)接口。 Framework 设备对象是在系统上设备的 framework 表示形式。 每个设备对象具有父驱动程序对象。

当系统中，新设备到达时，框架将调用[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法以通知到达和传递的驱动程序[IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)和[IWDFDeviceInitialize](https://msdn.microsoft.com/library/windows/hardware/ff556965)中调用的接口。 该驱动程序可以调用 IWDFDeviceInitialize 接口来初始化新的设备的方法。 例如，驱动程序调用[ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff556982)方法来查询有关设备安装的一部分提供的设备信息。 然后，该驱动程序可以调用[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法配置并创建设备对象。

当驱动程序创建 framework 设备对象时，它们可以将其[IPnpCallback](https://msdn.microsoft.com/library/windows/hardware/ff556762)， [IPnpCallbackSelfManagedIo](https://msdn.microsoft.com/library/windows/hardware/ff556776)， [IPnpCallbackHardware](https://msdn.microsoft.com/library/windows/hardware/ff556764)， [IFileCallbackCleanup](https://msdn.microsoft.com/library/windows/hardware/ff554902)，并[IFileCallbackClose](https://msdn.microsoft.com/library/windows/hardware/ff554907)接口。 清除和关闭的文件和插 (PnP) 和电源管理 (PM) 事件发生时，框架然后会通知驱动程序。 有关支持即插即用和 PM 的详细信息，请参阅[基于 UMDF 驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

 

 





