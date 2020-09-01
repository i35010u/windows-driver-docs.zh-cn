---
title: 用于 KMDF 驱动程序的 WMI 简介
description: 用于 KMDF 驱动程序的 WMI 简介
ms.assetid: e919f6c9-a4c5-4972-91e7-f4fa609455fe
keywords:
- WMI WDK KMDF
- WMI WDK KMDF，关于基于框架的驱动程序的 WMI
- 回调函数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2098da3601fed8c1d807c41a7190d90bc0033ed7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184277"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>用于 KMDF 驱动程序的 WMI 简介


\[仅适用于 KMDF\]

内核模式驱动程序框架支持提供信息的驱动程序， [Windows Management Instrumentation](../kernel/introduction-to-wmi.md) (WMI) 。 此类驱动程序称为 *wmi 数据提供* 程序，因为它们向 *wmi 客户端*提供数据，这些客户端是已注册为从 WMI 接收信息的应用程序。

WMI 数据提供程序支持 *wmi 数据块*，它可以代表以下一项或多项：

-   *数据项*，其中包含驱动程序向 WMI 客户端发送或从其接收的设备特定数据。

-    (函数的*方法*) 驱动程序代表 WMI 客户端执行。

-   驱动程序向已注册接收设备特定事件的通知的 WMI 客户端发送的*事件*。

在 mof 文件中，WMI 数据块被指定为 *wmi 类* 。 每个 WMI 数据块由 GUID 标识。

所有驱动程序都必须支持 WMI 为其设备类定义的任何标准 WMI 数据块。 这些 WMI 数据块是在 *Wmicore*中定义的。

你的驱动程序还可以支持你在 mof 文件中定义的 WMI 数据块。 若要了解如何定义和发布自定义的 WMI 数据块，请参阅以下部分：

-   [WMI 数据和事件块的 MOF 语法](../kernel/mof-syntax-for-wmi-data-and-event-blocks.md)

-   [设计 WMI 数据和事件块](../kernel/designing-wmi-data-and-event-blocks.md)

-   [发布 WMI 架构](../kernel/publishing-a-wmi-schema.md)

-   [WMI 属性表](../kernel/wmi-property-sheets.md)

### <a name="framework-wmi-objects-and-callback-functions"></a>框架 WMI 对象和回调函数

框架定义了两个对象，驱动程序可以使用这些对象来实现 WMI 数据提供程序。 *Wmi 提供程序对象*表示驱动程序提供的 wmi 数据块的架构。 *WMI 实例对象*表示与特定提供程序相关联的数据块的实例。 驱动程序通过实现以下两个对象定义的以下事件回调函数与 WMI 客户端进行通信：

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)  
启用和禁用驱动程序对收集 WMI 数据和发送 WMI 事件的支持。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)  
将 WMI 提供程序的实例数据传递到 WMI 客户端。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*EvtWmiInstanceSetInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)和[ *EvtWmiInstanceSetItem*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)  
将驱动程序的数据块中的信息设置为客户端提供的值。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)  
在客户端请求时执行驱动程序提供的方法。

### <a name="sample-drivers-that-implement-wmi"></a>实现 WMI 的示例驱动程序

FIREFLY、PCIDRV 和 Toaster [示例驱动程序](sample-kmdf-drivers.md) 为 WMI 数据提供程序。

 

