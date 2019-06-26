---
title: 将移动宽带应用与其他 Windows 组件集成
description: 将移动宽带应用与其他 Windows 组件集成
ms.assetid: 70469f6b-70a8-4ebc-b315-08ddeffbdc0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cad659cb3c38a81b3134cc539e278305dc1c9dc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359259"
---
# <a name="integrate-a-mobile-broadband-app-with-other-windows-components"></a>将移动宽带应用与其他 Windows 组件集成


可以使用 Windows 10 用户界面 (UI) 图面以增强你的移动宽带应用的整体体验。

布局、 导航、 命令、 动画、 触摸交互、 对齐和缩放、 协定和功能、 磁贴和通知的其他用户体验设计指南，UI 控件，应用程序漫游到云以及基础知识，请参阅[适用于 UWP 应用的索引的用户体验指南](https://developer.microsoft.com/windows/apps/design)。

本主题包含以下各节：

-   [应用设置](#app-settings)

-   [错误的用户体验](#errorux)

-   [应用视图](#appviews)

-   [启动点](#launchpts)

-   [磁贴和 toast 通知](#tileandtoast)

-   [初始屏幕](#splash)

-   [快速摘要](#qusum)

-   [其他资源](#resources)

## <a name="app-settings"></a>应用设置


可以使用[应用设置](https://docs.microsoft.com/windows/uwp/app-settings/guidelines-for-app-settings)以包括你的应用程序配置的设置。 其中的一些示例如下所示：

-   登录和注销

-   查看和编辑用户配置文件

-   更改帐单邮寄地址

-   查看和编辑支付选项

-   查看和设置市场营销首选项

## <a name="span-iderroruxspanspan-iderroruxspanerror-user-experience"></a><span id="errorux"></span><span id="ERRORUX"></span>错误的用户体验


### <a name="span-idgeneralspanspan-idgeneralspanspan-idgeneralspangeneral"></a><span id="General"></span><span id="general"></span><span id="GENERAL"></span>常规

移动宽带应用可以有许多应正常处理的错误情况。 一些常见示例是，如下所示：

-   **设备已丢失或拔出**SIM 或硬件保护装置等设备已丢失或拔出时显示。

-   **已锁定的设备**时连接的设备已锁定到该用户显示。

-   **Internet 连接丢失**时检测到没有网络连接时出现。

-   **插入多个设备**插入内置适配器和外部硬件保护装置时显示。 对于这种情况下，建议通知栏错误。

-   **窗体字段验证错误**时用户的表单中输入的信息不正确显示。 验证错误应内联显示，以便让用户知道该错误与之关联的字段。

有关如何存在错误的指导，请参阅[布置 UI](https://docs.microsoft.com/previous-versions/windows/apps/hh465304(v=win.10))。 在下面的示例中，通知栏显示在页面的顶部。

![通知栏会显示错误](images/mb-fig1-notificationbarerrors.png)

### <a name="span-iderrorsindatausagespanspan-iderrorsindatausagespanspan-iderrorsindatausagespanerrors-in-data-usage"></a><span id="Errors_in_data_usage"></span><span id="errors_in_data_usage"></span><span id="ERRORS_IN_DATA_USAGE"></span>中的数据使用情况的错误

以下的错误情况应按以下方式显示在概述页上：

-   **当用户是将要计划到期**:使用屏幕顶部的栏来指示用户计划即将到期。

-   **使用情况时通过数据上限**数据条应完整并且还应描述了该问题，并要执行的操作通知用户有关它的内联消息。 或者，over 数据上限用法消息可以是在页面顶部的通知栏中。

-   **该计划已过期时**:使用摘要框顶部栏来描述的问题和用户所能执行的操作。 在这种情况下，数据使用情况，计费周期，和漫游信息不会显示。

-   **国际漫游**:指示在摘要部分的底部漫游。

## <a name="span-idappviewsspanspan-idappviewsspanapp-views"></a><span id="appviews"></span><span id="APPVIEWS"></span>应用程序视图


您的应用程序应是自适应，并且能以容纳多的布局，包括：

-   Landscape

-   Portrait

-   与另一个应用程序并行

-   填充

-   键盘向上键

    **请注意**  当触摸键盘启动时，请确保元素，如窗体字段相应滚动。

     

以下示例显示同时另一个应用程序中某些页面的外观。

![与另一个应用程序并行的登陆页面](images/mb-fig2-snappedview-landingpage.png)

![与另一个应用程序并行服务页](images/mb-fig3-snappedview-servicespage.png)

请确保您的应用程序可通过应用程序视图，包括高对比度模式和屏幕读取器准备访问。 有关如何使您的应用程序可访问的详细信息，请参阅[中使用 JavaScript 的 UWP 应用的辅助功能](https://docs.microsoft.com/previous-versions/windows/apps/hh452681(v=win.10))。

## <a name="span-idlaunchptsspanspan-idlaunchptsspanlaunch-points"></a><span id="launchpts"></span><span id="LAUNCHPTS"></span>启动点


移动宽带应用可供用户在**所有应用**视图中的，在 Windows 连接管理器中，或通过一条 toast 通知。

![若要启动应用程序的入口点](images/mb-fig4-entrypoints.png)

### <a name="span-idlaunchfromwindowsconnectionmanagerspanspan-idlaunchfromwindowsconnectionmanagerspanspan-idlaunchfromwindowsconnectionmanagerspanlaunch-from-windows-connection-manager"></a><span id="Launch_from_Windows_Connection_Manager"></span><span id="launch_from_windows_connection_manager"></span><span id="LAUNCH_FROM_WINDOWS_CONNECTION_MANAGER"></span>启动从 Windows 连接管理器

![通过使用 windows 连接管理器中启动应用程序](images/mb-fig5-startfromwcm.png)

可以使用 Windows 连接管理器连接到移动宽带应用程序。 使用帐户和数据使用情况信息的登陆页面应打开你的应用。 在连接后，Windows 连接管理器将显示当前帐户和数据使用情况。

![windows 连接管理器帐户信息](images/mb-fig6-wcmaccountinfo.png)

**从连接管理器强制网络门户购买流期间自动启动**

当用户连接到强制网络门户网络 web 流量重定向到何处时，Windows 将提供自动启动自己的应用程序，如果已安装的选项。 应用程序应打开至购买 Internet 访问权限的方式提供信息的计划页。

### <a name="span-idlaunchappfromtileinallappsviewspanspan-idlaunchappfromtileinallappsviewspanspan-idlaunchappfromtileinallappsviewspanlaunch-app-from-tile-in-all-apps-view"></a><span id="Launch_app_from_tile_in_All_Apps_view"></span><span id="launch_app_from_tile_in_all_apps_view"></span><span id="LAUNCH_APP_FROM_TILE_IN_ALL_APPS_VIEW"></span>从所有应用视图中的磁贴启动应用

您的应用程序应支持具有多个同时进行帐户 （例如，使用两个外部 USB 移动宽带适配器） 的用户。 从磁贴启动你的应用时，您的应用程序应允许用户选择他们想要使用的帐户。

如果你的应用已挂起或已在运行，它应显示使用的最后一页。 如果您的应用程序不是已运行或挂起信息不可用，您的应用程序应打开到登录页。

### <a name="span-idtileandtoastspanspan-idtileandtoastspantile-and-toast-notifications"></a><span id="tileandtoast"></span><span id="TILEANDTOAST"></span>磁贴和 toast 通知

在中**启动**菜单中，磁贴是应用程序的主要表示形式。 用户启动应用程序通过这些磁贴可以显示通过通知新、 相关且定制的内容。 这使得**启动**菜单感觉充满活力，并允许用户查看最新信息一目了然。 应用还可以指定用户是否是在另一个应用中，在通信通过 toast 通知向用户的时间关键事件**启动**屏幕上，或在桌面上。 方法来设计和交付 toast 紧密地与磁贴，因此可降低学习难度。

![启动屏幕磁贴](images/mb-fig7-startscreentile.png)

Toast 通知可以包含文本和图像，但不是支持辅助操作，例如按钮。 将为类似于 Windows 气球状通知从任务栏的通知区域的 toast 通知。 气球状通知等屏幕的右下角将出现 toast 通知。 当用户点击或单击 toast 时，与通知相关的视图中启动的关联应用程序。 这是通过其中一个应用可能会中断另一个应用程序中的用户的唯一机制。 可以激活、 取消的或忽略用户 toast。 用户可以禁用所有应用的 toast。

![toast 通知](images/mb-fig8-toastonpage.png)

Toast 通知应仅用于高用户所需的信息，并且通常涉及某种形式的用户选择中。 它是一个不错选择传入电子邮件警报、 IM 聊天请求和突发新闻。 但是，它是非常重要，在你考虑使用 toast 通知，认识到，由于其暂时性的性质，用户可能永远不会看到它。 当使用超额数据使用情况或漫游警报 toast 通知，请考虑在最终用户未命中 toast 通知的情况下显示的信息在磁贴上并在应用视图中。

### <a name="span-idsplashspanspan-idsplashspansplash-screen"></a><span id="splash"></span><span id="SPLASH"></span>初始屏幕

初始屏幕可用于提升品牌。 有关初始屏幕的详细信息，请参阅[添加初始屏幕](https://docs.microsoft.com/previous-versions/windows/apps/hh465332(v=win.10))。

![初始屏幕](images/mb-fig4-splash-screen.png)

### <a name="span-idqusumspanspan-idqusumspanquick-summary"></a><span id="qusum"></span><span id="QUSUM"></span>快速摘要

运营商通知适合的设计：

-   使用这两个 toast 和磁贴的与订阅服务器的帐户和服务计划相关的重要和高利率消息警告用户通知。

-   自定义 toast 和磁贴背景颜色和徽标品牌准则。

-   包括重要的短信或 USSD 运营商通知和与直接在登录页上的订阅服务器的帐户和服务计划相关的警报。

运营商通知的设计不完善：

-   不显示 toast 通知不是实时 （如促销的播发） 的信息。

-   不显示用户与用户聊天消息和促销和运营商通知和警报，以及混合的播发，因为最终用户可能会错过重要的运营商通知。

### <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>其他资源

-   [使用磁贴、 锁屏提醒和 toast 通知](https://docs.microsoft.com/previous-versions/windows/apps/hh868259(v=win.10))

-   [指南和 toast 通知的核对清单](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-badges-notifications)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计用户体验的移动宽带应用程序](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






