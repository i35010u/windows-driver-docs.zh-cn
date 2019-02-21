---
title: 启用移动运营商通知和系统事件
description: 启用移动运营商通知和系统事件
ms.assetid: 988bafcc-ad8e-446d-9336-85c19cf05577
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e16f59242649b95b7eb19ca129babf43569b7bd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522603"
---
# <a name="enabling-mobile-operator-notifications-and-system-events"></a>启用移动运营商通知和系统事件


本主题提供有关移动操作员通知系统事件的信息。 它提供了指导原则，以便用于开发 UWP 移动宽带应用程序用于处理传入短信或基于 USSD 的移动运营商通知和相关移动宽带系统事件。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


客户的主移动宽带网络品牌体验是移动宽带应用。 此应用不需要提供管理功能的主连接，而是提供帐户的管理体验和服务的体验。 若要保留有关其帐户状态通知用户，应用程序必须执行一些活动，即使在用户不与它交互。 这些活动包括：

-   响应操作员 SMS 或网络启动 USSD 消息

-   通知用户他们已接近其数据限制

-   通知用户他们数据的计划已过期

-   通知用户其漫游状态

-   验证用户的数据计划是否支持 tethering

### <a name="span-idbackgroundbrokeredworkitemsspanspan-idbackgroundbrokeredworkitemsspanspan-idbackgroundbrokeredworkitemsspanbackground-brokered-work-items"></a><span id="Background_brokered_work_items"></span><span id="background_brokered_work_items"></span><span id="BACKGROUND_BROKERED_WORK_ITEMS"></span>中转的后台工作项

尽管 UWP 移动宽带应用程序可以运行全屏幕，但用户只应与在前台应用程序进行交互。 前台应用程序被假定为最重要到用户，使此应用程序接收的系统的所有资源。 如果应用不在前台，则它处于挂起状态并不能运行任何代码。 挂起应用程序保持暂停状态，直到用户在恢复它通过将返回到前台应用程序。 与此模型中的应用程序的行为，通过延迟或延迟，原因并不重要的后台应用程序的执行永远不会影响用户体验。 此外，减少不必要的后台活动优化了各种外观造型上的电池寿命。 若要恢复的挂起的应用程序所用的时间不计，将显示为大多数用户几乎不会被察觉。

Windows 10 提供了可以使应用程序磁贴保持最新即使应用已挂起的 Windows 推送通知。 推送通知进行了优化系统性能和延长设备电池寿命，因此最好是使用 Windows 推送通知，只要有可能。 如果挂起应用程序必须运行其自己的代码来执行其他类型的工作，您可以创建后台任务。

尽管 UWP 应用无法运行任何代码，如果它们不在前台运行，但可以使用系统事件代理应用处于后台时，运行代码以响应事件。 应用可以与系统事件代理，以响应特定背景中转事件注册工作项。 当后台中转事件触发，而不考虑应用程序的当前状态 （活动或挂起） 时，Windows 运行应用的工作项。

一般情况下，背景事件作为简单的触发点和不应发出信号处理量很大。 在这种情况下，为每个应用的配额将放置在允许的背景事件的处理时间。 提供由网络运算符 API 的后台事件包括[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件并[HotspotAuthentication](handling-the-hotspot-authentication-event.md)事件，会将 Windows 作为关键事件处理。 与常规背景事件相比，后台工作项与相关联**MobileOperatorNotification**并**HotspotAuthentication**事件运行而不考虑事件的每个实例尽管每个后台工作项实例受到处理时间配额的处理时间配额。 应该限制后台事件处理程序中的处理和推迟到移动宽带应用更大的处理。

## <a name="span-idinthissectionspanspan-idinthissectionspanspan-idinthissectionspanin-this-section"></a><span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>在本部分中


-   [开发用于处理 MobileOperatorNotification 事件的应用](develop-an-app-to-handle-the-mobileoperatornotification-event.md)

-   [移动运营商通知事件技术详细信息](mobile-operator-notification-event-technical-details.md)

-   [移动运营商通知方案](mobile-operator-notification-scenarios.md)

 

 





