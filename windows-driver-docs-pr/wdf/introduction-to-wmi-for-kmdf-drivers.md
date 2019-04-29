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
ms.openlocfilehash: 7ab7d04fdef5c59b7682f3780f03f5ba339c28b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388611"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>用于 KMDF 驱动程序的 WMI 简介


\[仅适用于 KMDF\]

内核模式驱动程序框架支持驱动程序的信息提供给[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff548187) (WMI)。 此类驱动程序被称为*WMI 数据提供程序*因为它们提供数据到*WMI 客户端*，这是已注册从 WMI 接收信息的应用程序。

WMI 数据访问接口支持*WMI 数据块*，前者表示一个或多个以下：

-   *数据项*，其中包含设备特定的驱动程序将发送到，或从 WMI 客户端接收的数据。

-   *方法*（函数） 驱动程序执行代表 WMI 客户端。

-   *事件*驱动程序发送到已注册接收通知的特定于设备的事件的 WMI 客户端。

WMI 数据块指定为*WMI 类*.mof 文件中。 每个 WMI 数据块是由 GUID 标识。

所有驱动程序必须支持其设备类的 WMI 定义任何标准 WMI 数据块。 这些 WMI 数据块中定义*Wmicore.mof*。

您的驱动程序还可以支持的.mof 文件中定义的 WMI 数据块。 若要了解如何定义和发布自定义的 WMI 数据块，请参阅以下各节：

-   [WMI 数据和事件块的 MOF 语法](https://msdn.microsoft.com/library/windows/hardware/ff556400)

-   [设计 WMI 数据和事件块](https://msdn.microsoft.com/library/windows/hardware/ff543036)

-   [发布 WMI 架构](https://msdn.microsoft.com/library/windows/hardware/ff559963)

-   [WMI 属性表](https://msdn.microsoft.com/library/windows/hardware/ff566368)

### <a name="framework-wmi-objects-and-callback-functions"></a>Framework WMI 对象和回调函数

框架定义驱动程序可用于实现 WMI 数据提供程序的两个对象。 *WMI 提供程序对象*表示 WMI 数据块的驱动程序提供的架构。 *WMI 实例对象*表示与特定的提供程序相关联的数据块的一个实例。 通过实现这两个对象定义的以下事件回调函数将与 WMI 客户端通信的驱动程序：

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff541855)  
启用和禁用对收集 WMI 数据和将 WMI 事件发送的驱动程序的支持。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](https://msdn.microsoft.com/library/windows/hardware/ff541843)  
传递到 WMI 客户端 WMI 提供程序的实例数据。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*EvtWmiInstanceSetInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541847)并[ *EvtWmiInstanceSetItem*](https://msdn.microsoft.com/library/windows/hardware/ff541852)  
在为客户提供值的驱动程序的数据块中设置的信息。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](https://msdn.microsoft.com/library/windows/hardware/ff541836)  
执行驱动程序所提供的方法，客户端的请求。

### <a name="sample-drivers-that-implement-wmi"></a>实现 WMI 的示例驱动程序

FIREFLY、 PCIDRV 和 Toaster[示例驱动程序](sample-kmdf-drivers.md)WMI 数据提供程序。

 

 





