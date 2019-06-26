---
title: 用于 KMDF 驱动程序的 WMI 简介
description: 用于 KMDF 驱动程序的 WMI 简介
ms.assetid: e919f6c9-a4c5-4972-91e7-f4fa609455fe
keywords:
- WMI WDK KMDF
- WMI WDK KMDF，有关 WMI 的基于框架的驱动程序
- 回调函数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83c58c615e5f92e45460b70dadf0e0c2fbacd9a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371110"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>用于 KMDF 驱动程序的 WMI 简介


\[仅适用于 KMDF\]

内核模式驱动程序框架支持驱动程序的信息提供给[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-wmi) (WMI)。 此类驱动程序被称为*WMI 数据提供程序*因为它们提供数据到*WMI 客户端*，这是已注册从 WMI 接收信息的应用程序。

WMI 数据访问接口支持*WMI 数据块*，前者表示一个或多个以下：

-   *数据项*，其中包含设备特定的驱动程序将发送到，或从 WMI 客户端接收的数据。

-   *方法*（函数） 驱动程序执行代表 WMI 客户端。

-   *事件*驱动程序发送到已注册接收通知的特定于设备的事件的 WMI 客户端。

WMI 数据块指定为*WMI 类*.mof 文件中。 每个 WMI 数据块是由 GUID 标识。

所有驱动程序必须支持其设备类的 WMI 定义任何标准 WMI 数据块。 这些 WMI 数据块中定义*Wmicore.mof*。

您的驱动程序还可以支持的.mof 文件中定义的 WMI 数据块。 若要了解如何定义和发布自定义的 WMI 数据块，请参阅以下各节：

-   [WMI 数据和事件块的 MOF 语法](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)

-   [设计 WMI 数据和事件块](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)

-   [发布 WMI 架构](https://docs.microsoft.com/windows-hardware/drivers/kernel/publishing-a-wmi-schema)

-   [WMI 属性表](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-property-sheets)

### <a name="framework-wmi-objects-and-callback-functions"></a>Framework WMI 对象和回调函数

框架定义驱动程序可用于实现 WMI 数据提供程序的两个对象。 *WMI 提供程序对象*表示 WMI 数据块的驱动程序提供的架构。 *WMI 实例对象*表示与特定的提供程序相关联的数据块的一个实例。 通过实现这两个对象定义的以下事件回调函数将与 WMI 客户端通信的驱动程序：

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)  
启用和禁用对收集 WMI 数据和将 WMI 事件发送的驱动程序的支持。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)  
传递到 WMI 客户端 WMI 提供程序的实例数据。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*EvtWmiInstanceSetInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)并[ *EvtWmiInstanceSetItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)  
在为客户提供值的驱动程序的数据块中设置的信息。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)  
执行驱动程序所提供的方法，客户端的请求。

### <a name="sample-drivers-that-implement-wmi"></a>实现 WMI 的示例驱动程序

FIREFLY、 PCIDRV 和 Toaster[示例驱动程序](sample-kmdf-drivers.md)WMI 数据提供程序。

 

 





