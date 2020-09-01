---
title: 将移动宽带应用与其他 Windows 组件集成
description: 将移动宽带应用与其他 Windows 组件集成
ms.assetid: 70469f6b-70a8-4ebc-b315-08ddeffbdc0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9679b08a86f242b7fdbfe93151c4f38cd5106ac9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215296"
---
# <a name="integrate-a-mobile-broadband-app-with-other-windows-components"></a>将移动宽带应用与其他 Windows 组件集成


可以使用 Windows 10 用户界面 (UI) 图面来增强移动宽带应用程序的总体体验。

有关布局、导航、命令、动画、触摸交互、对齐和缩放、协定和功能、磁贴和通知、UI 控件、到云的应用程序漫游的其他用户体验设计指南，请参阅 [UWP 应用的 UX 准则索引](https://developer.microsoft.com/windows/apps/design)。

本主题包含以下各节：

-   [应用设置](#app-settings)

-   [用户体验错误](#errorux)

-   [应用视图](#appviews)

-   [启动点](#launchpts)

-   [磁贴和 toast 通知](#tileandtoast)

-   [初始屏幕](#splash)

-   [快速摘要](#qusum)

-   [其他资源](#resources)

## <a name="app-settings"></a>应用设置


你可以使用 [应用设置](/windows/uwp/app-settings/guidelines-for-app-settings) 来包括应用配置的设置。 其中的一些示例如下所示：

-   登录和注销

-   查看和编辑用户配置文件

-   更改计费地址

-   查看和编辑付款选项

-   查看和设置市场营销首选项

## <a name="span-iderroruxspanspan-iderroruxspanerror-user-experience"></a><span id="errorux"></span><span id="ERRORUX"></span>用户体验错误


### <a name="span-idgeneralspanspan-idgeneralspanspan-idgeneralspangeneral"></a><span id="General"></span><span id="general"></span><span id="GENERAL"></span>常规

你的移动宽带应用可能会有很多错误案例，它们应该妥善处理。 一些常见示例如下所示：

-   **设备已丢失或已拔** 出当设备（例如 SIM 或转换器）丢失或拔下时出现。

-   **锁定的设备** 已连接的设备锁定到用户时出现。

-   **Internet 连接丢失** 未检测到网络连接时显示。

-   **已插入多个设备** 插入内置适配器和外部转换器时出现。 对于这种情况，建议使用通知栏错误。

-   **表单域验证错误** 当用户向窗体中输入不正确的信息时显示。 验证错误应以内联方式显示，以便用户知道与错误关联的字段。

有关如何显示错误的指南，请参阅对 [UI 进行布局](/previous-versions/windows/apps/hh465304(v=win.10))。 在下面的示例中，页面顶部将显示一个通知栏。

![通知栏显示错误](images/mb-fig1-notificationbarerrors.png)

### <a name="span-iderrors_in_data_usagespanspan-iderrors_in_data_usagespanspan-iderrors_in_data_usagespanerrors-in-data-usage"></a><span id="Errors_in_data_usage"></span><span id="errors_in_data_usage"></span><span id="ERRORS_IN_DATA_USAGE"></span>数据使用中的错误

以下错误事例应显示在 "概述" 页上，如下所示：

-   **当用户接近计划过期时**：使用屏幕顶部的栏表示用户的计划接近过期。

-   **当使用量超过数据上限时** 数据条应是完整的，而且还应该有描述该问题的内联消息，并告知用户要如何处理该问题。 或者，通过数据上限使用消息可以在页面顶部的通知栏中进行。

-   **当计划过期时**：在 "摘要" 框顶部使用栏来描述用户可以采取的问题和操作。 在这种情况下，不显示数据使用情况、计费周期和漫游信息。

-   **国际漫游**：指示 "摘要" 部分底部的 "漫游"。

## <a name="span-idappviewsspanspan-idappviewsspanapp-views"></a><span id="appviews"></span><span id="APPVIEWS"></span>应用视图


您的应用程序应该是自适应的，能够适应多个布局，其中包括：

-   横向

-   纵向

-   与另一个应用并行

-   灰色

-   向上键盘

    **注意**   触摸键盘启动时，请确保元素（如窗体字段）正确滚动。

     

下面的示例演示了某些页面与其他应用并行的外观。

![与其他应用并行的登录页](images/mb-fig2-snappedview-landingpage.png)

![与其他应用并行的服务页](images/mb-fig3-snappedview-servicespage.png)

请确保可以通过应用视图访问应用，包括高对比度模式和屏幕阅读器准备情况。 有关如何使应用程序可访问的详细信息，请参阅 [使用 JavaScript 的 UWP 应用中的辅助功能](/previous-versions/windows/apps/hh452681(v=win.10))。

## <a name="span-idlaunchptsspanspan-idlaunchptsspanlaunch-points"></a><span id="launchpts"></span><span id="LAUNCHPTS"></span>启动点


你的移动宽带应用可供用户在 " **所有应用** " 视图、"Windows 连接管理器" 或 "通过 toast 通知" 中使用。

![入门应用程序的入口点](images/mb-fig4-entrypoints.png)

### <a name="span-idlaunch_from_windows_connection_managerspanspan-idlaunch_from_windows_connection_managerspanspan-idlaunch_from_windows_connection_managerspanlaunch-from-windows-connection-manager"></a><span id="Launch_from_Windows_Connection_Manager"></span><span id="launch_from_windows_connection_manager"></span><span id="LAUNCH_FROM_WINDOWS_CONNECTION_MANAGER"></span>从 Windows 连接管理器启动

![使用 windows 连接管理器启动应用程序](images/mb-fig5-startfromwcm.png)

可以使用 Windows 连接管理器连接到移动宽带应用。 应用应使用帐户和数据使用信息打开登录页。 连接后，Windows 连接管理器将显示当前帐户和数据的使用情况。

![windows 连接管理器帐户信息](images/mb-fig6-wcmaccountinfo.png)

**在捕获的门户购买流程中从连接管理器自动启动**

如果用户连接到将 web 流量重定向到的固定门户网络，Windows 会提供选项，以便在安装应用程序时自动启动其应用。 应用应打开 "计划" 页，其中提供了有关如何购买 Internet 访问的信息。

### <a name="span-idlaunch_app_from_tile_in_all_apps_viewspanspan-idlaunch_app_from_tile_in_all_apps_viewspanspan-idlaunch_app_from_tile_in_all_apps_viewspanlaunch-app-from-tile-in-all-apps-view"></a><span id="Launch_app_from_tile_in_All_Apps_view"></span><span id="launch_app_from_tile_in_all_apps_view"></span><span id="LAUNCH_APP_FROM_TILE_IN_ALL_APPS_VIEW"></span>在所有应用视图中从磁贴启动应用

应用应支持具有多个同时帐户的用户 (例如，使用两个外部 USB 移动宽带适配器) 。 从磁贴启动应用时，应用应允许用户选择他们想要使用的帐户。

如果你的应用程序已挂起或已在运行，则它应显示最后使用的页。 如果你的应用程序尚未运行或挂起信息不可用，则你的应用程序应打开到登陆页面。

### <a name="span-idtileandtoastspanspan-idtileandtoastspantile-and-toast-notifications"></a><span id="tileandtoast"></span><span id="TILEANDTOAST"></span>磁贴和 toast 通知

在 " **开始** " 菜单中，磁贴是应用的主要表示形式。 用户通过这些磁贴启动其应用，这些磁贴可以通过通知显示新的相关内容和定制内容。 这使 " **开始** " 菜单显得非常生动，并使用户能够一目了然地查看新增内容。 应用还可以通过 toast 通知将时间关键事件与用户通信，无论用户是在其他应用中、在 " **开始** " 屏幕上，还是在桌面上。 设计和交付 toast 的方法与磁贴的设计方法非常相似，因此降低了学习曲线。

![启动屏幕磁贴](images/mb-fig7-startscreentile.png)

Toast 通知可以包含文本和图像，但不支持按钮等辅助操作。 将 toast 视为类似于任务栏通知区域中的 Windows 气球通知。 与气球通知类似，屏幕右下角会出现一个 toast。 当用户点击或单击 toast 时，相关联的应用程序将在与通知相关的视图中启动。 这是一个应用可以中断另一个应用中的用户的唯一机制。 用户可以激活、解除或忽略 toast。 用户可以禁用应用程序的所有 toast。

![toast 通知](images/mb-fig8-toastonpage.png)

Toast 通知应仅用于对用户感兴趣的信息，并且通常涉及某种形式的用户选择加入。 对于传入电子邮件警报、IM 聊天请求和突发新闻，这是一个不错的选择。 但是，在考虑使用 toast 通知时，这一点非常重要，因为它的暂时性性质，用户可能永远看不到它。 使用 toast 通知进行数据使用超额或漫游警报时，请考虑在最终用户未命中 toast 通知的情况下，在你的磁贴和应用视图中显示信息。

### <a name="span-idsplashspanspan-idsplashspansplash-screen"></a><span id="splash"></span><span id="SPLASH"></span>初始屏幕

您可以使用初始屏幕来升级品牌。 有关初始屏幕的详细信息，请参阅 [添加初始屏幕](/previous-versions/windows/apps/hh465332(v=win.10))。

![初始屏幕](images/mb-fig4-splash-screen.png)

### <a name="span-idqusumspanspan-idqusumspanquick-summary"></a><span id="qusum"></span><span id="QUSUM"></span>快速摘要

适用于操作员通知的设计：

-   使用 toast 和磁贴通知向用户通知与订阅者的帐户和服务计划相关的重要和高兴趣消息。

-   根据品牌准则自定义 toast 和磁贴背景颜色和徽标。

-   直接在登陆页面上包含与订阅者的帐户和服务计划相关的重要短信或 USSD 操作员通知和警报。

运算符通知设计不当：

-   对于不是实时 (如) 促销广告的信息，请勿显示 toast 通知。

-   不要显示与操作员通知和警报一起混合的用户到用户聊天消息和促销和播发，因为最终用户可能会错过重要的操作员通知。

### <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>其他资源

-   [使用磁贴、徽章和 toast 通知](/previous-versions/windows/apps/hh868259(v=win.10))

-   [Toast 通知的指导原则和核对清单](/windows/uwp/controls-and-patterns/tiles-badges-notifications)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

