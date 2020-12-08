---
title: 使用自定义 WMI 事件
description: 使用自定义 WMI 事件
keywords:
- WMI WDK 内核，事件跟踪
- 事件 WDK WMI
- 跟踪 WDK WMI
- 发送 WMI 事件
- 事件块 WDK WMI
- 通知 WDK WMI
- 事件使用者提供程序 WDK WMI
- 自定义事件 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cb4ec1f55cf94584198a84201aeed3ad6e55d10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825585"
---
# <a name="using-custom-wmi-events"></a>使用自定义 WMI 事件





支持某些 WMI 事件类需要某些驱动程序类。 驱动程序还可以设计自己的自定义 WMI 事件类。 自定义 WMI 事件为驱动程序提供了一种将数据传递回用户模式组件的方法。 用户模式组件通过 WMI COM 接口接收 WMI 事件。

应用程序可以接收事件通知，如下所示：

-   使用 **CoCreateInstance** 例程获取指向 **IWbemLocator** 对象的指针。

-   使用 **IWbemLocator** 指针连接到 WMI 服务器进程。 **IWBemLocator：： ConnectServer** 方法调用提供指向 **IWbemServices** 对象的指针。

-   使用 **IWbemServices** 对象来查询感兴趣的事件类型。 **IWbemServices：： ExecNotificationQuery** 方法允许您在 WMI 查询语言 (WQL) 中指定事件查询。

-   应用程序还可以通过实现 **IWbemObjectSink** 接口，注册以异步接收 WMI 事件。 应用程序使用 **IWbemServices：： ExecNotificationQueryAsync** 方法注册事件的异步通知。 当匹配事件发生时，系统将使用 **IWbemObjectSink：：指示** 方法通知应用程序发生的事件。

还可以实现用户模式 WMI *事件使用者提供程序*。 这是一个用户模式组件，在指定类型的事件发生时，WMI 可以自动加载该组件。

-   在用户模式组件的 MOF 数据中包含 **\_ \_ EventConsumerProviderRegistration** WMI 类的实例。

-   为要接收通知的每个 WMI 事件类实现 **IWbemUnboundObjectSink** 接口。

-   实现 **IWbemEventConsumerProvider** 接口可指定组件接收通知的事件类，以及关联的 **IWbemUnboundObjectSink** 实现。

-   实现将组件初始化为事件使用者的 **IWbemProviderInit** 接口。

Microsoft Windows SDK 文档中可以找到有关接收 WMI 事件和 **IWbemXxx** COM 接口的详细信息。

WMI 事件不是在发生特定情况时通知用户模式应用程序的唯一方法。 驱动程序可以实现应用程序可用于轮询通知的 IOCTL。 驱动程序和应用程序可以共享通知事件对象 (参阅 [事件对象](event-objects.md)) ，以指示发生了特定情况。

WMI 事件具有与这些其他方法相比的一些优点：

-   如果用户模式应用程序轮询事件的速度比驱动程序可以响应的速度更快，则驱动程序可能有很多 IOCTLs 挂起。

-   您可以通过使用通知事件对象通知用户模式应用程序来寻求解决之前的问题，但通知事件只会发出事件已发生的信号。 应用程序仍必须使用 IOCTL 才能获取任何其他数据。 接下来的两个问题仍适用。

-   如果多个应用程序轮询驱动程序的事件，则驱动程序将需要维护状态以确定哪些应用程序已接收了哪些事件。

-   某些驱动程序（如 SCSI 微型端口和 NDIS 微型端口驱动程序）无法接收 IOCTLs。

WMI 事件确实有一个缺点，即必须提供的用户模式代码比其他方法更复杂。

 

 




