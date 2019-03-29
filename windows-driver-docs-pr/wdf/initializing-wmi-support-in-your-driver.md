---
title: 在驱动程序中初始化 WMI 支持
description: 在驱动程序中初始化 WMI 支持
ms.assetid: cf79176c-8e08-45f9-b2fb-a82707d8667b
keywords:
- WMI WDK KMDF，初始化支持
- 提供程序实例 WDK KMDF
- 多个提供程序实例 WDK KMDF
- 单个提供程序实例 WDK KMDF
- 注册 MOF 资源名称 WDK KMDF
- MOF 资源名称 WDK KMDF
- 初始化 WMI 支持 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16023a6ebe0452eefbe68c8a8a02c993f54095df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565382"
---
# <a name="initializing-wmi-support-in-your-driver"></a>在驱动程序中初始化 WMI 支持


\[仅适用于 KMDF\]

若要支持 WMI 数据块，基于框架的驱动程序：

-   注册自定义的任何托管的对象格式 (MOF) 的资源名称中未定义的 WMI 数据提供程序*Wmicore.mof*。

-   创建要表示它可以读取或写入的数据块的一个或多个 WMI 实例对象。

-   根据需要实现一个或多个事件回调函数来提供驱动程序提供的 WMI 数据。

-   将每个 WMI 实例对象，以使其可供 WMI 客户端注册。

若要初始化其 WMI 支持，KMDF 驱动程序遵循这些步骤中，通常在其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)或[ *EvtDeviceSelfManagedIoInit*](https://msdn.microsoft.com/library/windows/hardware/ff540902)回调：

1.  提供了一个 MOF 文件以支持自定义的 WMI 数据提供程序的驱动程序必须调用[ **WdfDeviceAssignMofResourceName** ](https://msdn.microsoft.com/library/windows/hardware/ff545897)方法，该驱动程序创建 WMI 提供程序之前将 MOF 资源名称表示数据访问接口的对象。

2.  初始化 WMI 提供程序配置结构，并 （可选） 创建的 WMI 提供程序对象 (WDFWMIPROVIDER)。
3.  初始化 WMI 实例配置结构，并创建一个 WMI 实例对象 (WDFWMIINSTANCE)。

当 KMDF 驱动程序创建其第一个 WMI 实例时，框架默认情况下创建 WMI 提供程序。 因此，如果该驱动程序要求只有一个 WMI 提供程序，它不需要调用提供程序创建方法 ([**WdfWmiProviderCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551193))。 但是，该驱动程序必须填写提供程序配置结构，因为此结构提供了有关创建实例时，框架使用的提供程序的信息。

如果您的驱动程序创建的每个 WMI 数据块的单一实例，它支持，驱动程序调用[ **WdfWmiInstanceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551178)，将同时传递[ **WDF\_WMI\_提供程序\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff553067)结构和一个[ **WDF\_WMI\_实例\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff553058)结构。 此单个调用同时配置单个框架提供 WMI 提供程序对象，并创建一个 WMI 实例对象。

如果您的驱动程序创建其 WMI 数据块的多个实例，该驱动程序必须调用[ **WdfWmiProviderCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551193)并[ **WdfWmiInstanceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551178)

### <a href="" id="registering-provider-instances"></a> 注册提供程序实例

WMI 客户端可以访问您的驱动程序的 WMI 数据块之前，该驱动程序必须与系统的 WMI 服务注册其提供程序实例。 该驱动程序可以使用以下方法之一注册提供程序实例：

-   设置**注册**提供程序实例的成员[ **WDF\_WMI\_实例\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff553058)结构 **，则返回 TRUE**。

    如果您的驱动程序设置**注册**到**TRUE**，框架会自动注册该实例第一次，则设备将进入其工作 (D0) 状态。

-   调用[ **WdfWmiInstanceRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff551190)方法。

    如果您的驱动程序调用[ **WdfWmiInstanceRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff551190)后调用[ **WdfWmiInstanceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551178)，框架将注册实例设备后在其工作 (D0) 状态。

移除该实例的设备后，框架将自动注销每个提供程序实例 (和调用之前[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)事件回调函数)。 框架将在其中调用驱动程序的回调函数的顺序有关的信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

您的驱动程序可以取消注册实例在任何时候通过调用[ **WdfWmiInstanceDeregister**](https://msdn.microsoft.com/library/windows/hardware/ff551179)。

 

 





