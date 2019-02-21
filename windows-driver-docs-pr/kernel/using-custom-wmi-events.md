---
title: 使用自定义 WMI 事件
description: 使用自定义 WMI 事件
ms.assetid: 00354e0b-a652-44e9-8b2b-fd755cc05fec
keywords:
- WMI WDK 内核事件跟踪
- WDK WMI 事件
- 跟踪 WDK WMI
- 发送的 WMI 事件
- 事件阻止 WDK WMI
- 通知 WDK WMI
- 事件使用者提供程序 WDK WMI
- 自定义事件 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 792beb8c0a4541ef0803eac279e439ea14895d05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543031"
---
# <a name="using-custom-wmi-events"></a>使用自定义 WMI 事件





支持某些 WMI 事件类所需的驱动程序的一些类。 驱动程序还可以设计自己的自定义 WMI 事件类。 自定义 WMI 事件提供的驱动程序将数据传递回给用户模式组件一种方法。 用户模式组件接收 WMI 事件通过 WMI COM 接口。

应用程序可以接收事件通知，如下所示：

-   使用**CoCreateInstance**例程，以获取指向的指针**IWbemLocator**对象。

-   使用**IWbemLocator**用于连接到 WMI 服务器进程的指针。 **IWBemLocator::ConnectServer**方法调用为您提供一个指向**IWbemServices**对象。

-   使用**IWbemServices**感兴趣的事件类型的查询的对象。 **IWbemServices::ExecNotificationQuery**方法，可指定在 WMI 查询语言 (WQL) 的事件查询。

-   应用程序还可以注册以接收 WMI 事件以异步方式，通过实现**IWbemObjectSink**接口。 应用程序使用**iwbemservices:: Execnotificationqueryasync**方法注册的事件的异步通知。 匹配的事件发生时，系统将使用**IWbemObjectSink::Indicate**方法以通知发生的事件的应用程序。

您还可以实现用户模式下 WMI*事件使用者提供程序*。 这是 WMI 可以自动加载的指定类型的事件发生时的用户模式组件。

-   包含的实例 **\_ \_EventConsumerProviderRegistration**用户模式组件的 MOF 数据中的 WMI 类。

-   实现**IWbemUnboundObjectSink**为每个你想要接收的通知的 WMI 事件类的接口。

-   实现**IWbemEventConsumerProvider**接口来指定事件的类组件接收通知，以及关联**IWbemUnboundObjectSink**实现。

-   实现**IWbemProviderInit**初始化您的组件作为事件使用者的接口。

有关接收 WMI 事件的详细信息和**IWbemXxx** Microsoft Windows SDK 文档中找不到 COM 接口。

WMI 事件不是特定情况发生时通知用户模式应用程序的唯一方法。 驱动程序可以实现应用程序可用于轮询通知 IOCTL。 驱动程序和应用程序可以共享通知事件对象 (请参阅[事件对象](event-objects.md)) 以指示已发生的特定的情况。

WMI 事件具有超过这些其他方法的一些优势：

-   如果用户模式应用程序不是驱动程序可以响应更快地轮询事件，该驱动程序可能具有许多 Ioctl 挂起。

-   可以通过使用通知事件对象以通知用户模式应用程序，改善上一个问题，但通知事件可以仅发出已发生事件的信号。 应用程序仍必须使用 IOCTL 来获取任何其他数据。 接下来两个问题仍适用。

-   如果多个应用程序会轮询事件的驱动程序，该驱动程序需要维护状态，以确定哪些应用程序以前接收了哪些事件。

-   某些驱动程序，如 SCSI 微型端口和 NDIS 微型端口驱动程序，不能接收 Ioctl。

你必须提供的用户模式代码是复杂得多比其他方法的缺点是会 WMI 事件。

 

 




