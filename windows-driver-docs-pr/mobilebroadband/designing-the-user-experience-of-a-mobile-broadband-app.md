---
title: 设计移动宽带应用的用户体验简介
description: 设计移动宽带应用的用户体验简介
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2c8b19c313695a013b6586f3958e4ca156dc19f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782395"
---
# <a name="introduction-to-designing-the-user-experience-of-a-mobile-broadband-app"></a>设计移动宽带应用的用户体验简介


本主题提供有关如何设计适用于 Windows 10 的 UWP mobile 宽带应用程序的信息。 它提供用户体验设计指南，以便为用户设计用于管理移动宽带帐户和服务的应用。 它假定你熟悉移动宽带技术、Windows 移动宽带网络和 Microsoft Store 应用平台。

本主题中提供了以下各节：

-   [关键方案](#keyui)

-   [应用组织](#apporg)

-   [其他资源](#resources)

## <a name="span-idkeyuispanspan-idkeyuispankey-scenarios"></a><span id="keyui"></span><span id="KEYUI"></span>关键方案


移动宽带应用应包含以下关键方案：

-   **计划购买**

    -   购买新的数据服务订阅。

    -   将帐户余额重填到计划。

-   **帐户管理** 显示帐户数据和当前计划信息。

-   **查看数据使用情况**

    -   显示当前数据使用情况和计费周期信息。

    -   使用最新的数据使用情况更新 Windows。

-   **通知** 显示数据使用情况和其他重要的帐户和服务消息。

-   **帮助和支持** 显示故障排除和客户支持联系人信息。

## <a name="span-idapporgspanspan-idapporgspanapp-organization"></a><span id="apporg"></span><span id="APPORG"></span>应用组织


下面显示了如何组织应用中的不同页面：

![概览](images/mb-fig1-overview-uwp-device-app.png)

-   该应用程序具有帐户概述登录页，该页面提供客户帐户和数据使用情况的摘要。 它还包含指向其他应用程序页面的链接。

-   在登录页中，最终用户可以访问中心页来查看计费、计划、服务或帮助和支持详细信息。

-   某些中心页面将导致任务页和流，如购买结帐流。

**提示**  
对于预付计划，帐户概述可以直接链接到用于重填方案的 **付款** 页。

 

有关如何设计这些页的详细信息，请参阅以下主题：

-   [设计移动宽带应用的登陆页面](design-the-landing-page-of-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的品牌](design-branding-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的帐户余额和使用情况信息](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的消息](design-messages-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的计费页面](design-billing-pages-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的购买流](design-purchase-flows-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的帮助和支持页面](design-help-and-support-pages-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的服务和产品页面](design-services-and-goods-pages-in-a-mobile-broadband-app.md)

-   [将移动宽带应用与其他 Windows 组件集成](integrate-a-mobile-broadband-app-with-other-windows-components.md)

## <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>其他资源


-   [UWP 应用的 UX 准则索引](https://developer.microsoft.com/windows/apps/design)

-   [移动宽带概述](overview-of-mobile-broadband.md)

 

 





