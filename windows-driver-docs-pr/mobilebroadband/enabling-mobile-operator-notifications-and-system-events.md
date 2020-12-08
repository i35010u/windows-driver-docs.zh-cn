---
title: 启用移动运营商通知和系统事件的简介
description: 启用移动运营商通知和系统事件的简介
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: a5c17f58bd39875a123f8905730d784cc85e2346
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782359"
---
# <a name="introduction-to-enabling-mobile-operator-notifications-and-system-events"></a>启用移动运营商通知和系统事件的简介


本主题提供有关移动运营商通知系统事件的信息。 它为你提供了一些指导，让你开发用于处理传入 SMS 或基于 USSD 的移动运营商通知和相关移动宽带系统事件的 UWP mobile 宽带应用。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


客户的移动宽带网络品牌的主要体验是移动宽带应用。 此应用程序不应提供主要连接管理功能，而是提供帐户管理体验和服务体验。 若要使用户了解其帐户状态，应用必须执行某些活动，即使用户不与它交互也是如此。 这些活动包括：

-   响应操作员短信或网络启动的 USSD 消息

-   通知用户他们已接近其数据限制

-   通知用户其数据计划已过期

-   通知用户漫游状态

-   验证用户的数据计划是否支持 tethering

### <a name="span-idbackground_brokered_work_itemsspanspan-idbackground_brokered_work_itemsspanspan-idbackground_brokered_work_itemsspanbackground-brokered-work-items"></a><span id="Background_brokered_work_items"></span><span id="background_brokered_work_items"></span><span id="BACKGROUND_BROKERED_WORK_ITEMS"></span>后台中转工作项

尽管 UWP mobile 宽带应用可以全屏运行，但用户只应与前景中的应用程序交互。 假定前景应用对于用户是最重要的，因此此应用接收系统的所有资源。 当应用程序不在前台时，它会被挂起并且无法运行任何代码。 挂起的应用程序将保持挂起状态，直到用户通过将应用程序恢复到前台。 使用此应用程序行为模型，用户体验从不受执行不重要背景应用引起的滞后或延迟的影响。 此外，减少不必要的后台活动会优化各种外形规格的电池寿命。 恢复已挂起的应用程序所需的时间可忽略不计，并接近大多数用户的难察觉。

Windows 10 提供 Windows 推送通知，即使应用程序已挂起，也可以使应用程序磁贴保持最新状态。 推送通知经过优化，可实现系统性能和更长的设备电池寿命，因此最好尽可能使用 Windows 推送通知。 如果已挂起的应用程序必须运行其自己的代码来执行其他类型的工作，则可以创建后台任务。

尽管 UWP 应用不能在前台运行任何代码，但当应用处于后台时，系统事件代理允许您运行代码来响应事件。 应用可以向系统事件代理注册工作项，以响应特定的后台中转事件。 当触发后台中转事件时，Windows 将运行应用的工作项，而不考虑应用的当前状态 (活动或挂起) 。

通常情况下，后台事件旨在用作简单的触发器点，并不用于处理大量处理。 因此，每个应用的配额置于允许用于后台事件的处理时间。 网络操作员 API 提供的后台事件（包括 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件和 [HotspotAuthentication](handling-the-hotspot-authentication-event.md) 事件）被 Windows 视为关键事件。 与一般背景事件相比，与 **MobileOperatorNotification** 和 **HotspotAuthentication** 事件关联的后台工作项会对事件的每个实例运行，而不考虑处理时间配额，尽管后台工作项的每个实例都受处理时间配额的限制。 应在后台事件处理程序中限制处理，并将更大的处理推迟到移动宽带应用。

## <a name="span-idin_this_sectionspanspan-idin_this_sectionspanspan-idin_this_sectionspanin-this-section"></a><span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>本节内容


-   [开发用于处理 MobileOperatorNotification 事件的应用](develop-an-app-to-handle-the-mobileoperatornotification-event.md)

-   [移动运营商通知事件技术详细信息](mobile-operator-notification-event-technical-details.md)

-   [移动运营商通知方案](mobile-operator-notification-scenarios.md)

 

 





