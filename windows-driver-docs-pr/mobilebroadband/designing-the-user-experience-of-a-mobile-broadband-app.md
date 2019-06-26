---
title: 设计移动宽带应用的用户体验
description: 设计移动宽带应用的用户体验
ms.assetid: c84e2814-69ba-4cd0-ba11-1b035ccdfbde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30e2494c1684b42ef518e366ce29c388cc6fdf14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381529"
---
# <a name="designing-the-user-experience-of-a-mobile-broadband-app"></a>设计移动宽带应用的用户体验


本主题提供有关如何设计适用于 Windows 10 UWP 移动宽带应用程序的信息。 它提供了用户体验设计指南来设计适用于用户管理其移动宽带帐户和服务应用程序。 它假定你熟悉移动宽带技术、 Windows 移动宽带网络和 Microsoft Store 应用程序平台。

本主题中提供了以下各节：

-   [关键方案](#keyui)

-   [应用程序的组织](#apporg)

-   [其他资源](#resources)

## <a name="span-idkeyuispanspan-idkeyuispankey-scenarios"></a><span id="keyui"></span><span id="KEYUI"></span>关键方案


移动宽带应用程序应包括以下主要方案：

-   **计划购买**

    -   购买新订阅向数据服务。

    -   重新填充到计划的帐户余额。

-   **帐户管理**显示帐户数据和当前的计划信息。

-   **查看数据使用情况**

    -   显示当前数据使用情况和计费周期的信息。

    -   使用最新数据使用情况更新 Windows。

-   **通知**显示数据的使用情况和其他重要的帐户和服务消息。

-   **帮助和支持**显示疑难解答和客户支持联系信息。

## <a name="span-idapporgspanspan-idapporgspanapp-organization"></a><span id="apporg"></span><span id="APPORG"></span>应用程序的组织


下面的示例演示在应用程序如何将不同的页进行组织：

![概述](images/mb-fig1-overview-uwp-device-app.png)

-   应用程序具有提供的客户的帐户和数据使用情况摘要的帐户概览登陆页。 它还包含指向其他应用程序页。

-   从登录页中，最终用户可以访问中心页，查看计费、 计划、 服务或帮助和支持详细信息。

-   某些中心页会导致任务页和流，如采购结帐流程。

**提示**  的预付计划帐户概述可以直接链接到**付款**重填方案页。

 

有关如何设计这些页面的详细信息，请参阅以下主题：

-   [设计移动宽带应用程序的登录页](design-the-landing-page-of-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的品牌](design-branding-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的帐户余额和使用情况信息](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的消息](design-messages-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的计费页面](design-billing-pages-in-a-mobile-broadband-app.md)

-   [移动宽带应用中设计购买流](design-purchase-flows-in-a-mobile-broadband-app.md)

-   [设计帮助和支持的移动宽带应用中的页面](design-help-and-support-pages-in-a-mobile-broadband-app.md)

-   [设计移动宽带应用中的服务和产品页](design-services-and-goods-pages-in-a-mobile-broadband-app.md)

-   [与其他 Windows 组件集成，移动宽带应用](integrate-a-mobile-broadband-app-with-other-windows-components.md)

## <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>其他资源


-   [适用于 UWP 应用的索引的用户体验指南](https://developer.microsoft.com/windows/apps/design)

-   [移动宽带概述](overview-of-mobile-broadband.md)

 

 





