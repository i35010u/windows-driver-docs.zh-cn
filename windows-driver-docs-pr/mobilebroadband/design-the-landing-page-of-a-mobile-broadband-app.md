---
title: 设计移动宽带应用的登陆页面
description: 设计移动宽带应用的登陆页面
ms.assetid: 3a42886f-8a32-4576-af31-65443bb718ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a861764fd6a17a4c750c8cccfcc2e982d3780b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215329"
---
# <a name="design-the-landing-page-of-a-mobile-broadband-app"></a>设计移动宽带应用的登陆页面


登录页是用户在启动移动宽带应用时看到的第一个页面，只不过将 [移动宽带应用与其他 Windows 组件集成](integrate-a-mobile-broadband-app-with-other-windows-components.md#launchpts)中介绍的某些情况除外。

![登陆页面损失较大](images/mb-fig1-landing-page-postpaid.png)

登录页应遵循适用于应用布局的 UWP 应用指导原则。 为了鼓励简易性和便于导航，我们建议您将登陆页的所有内容都放入单个页面。 登陆页面是应用的中心。 尽管它不是主导航方法或管理页，但它会展示您的应用程序及其主要功能。

以下部分介绍了可在登陆页面中包含的某些内容：

-   [用法–显示概述或链接](#usageov)

-   [操作员消息–显示概述或链接](#opmsg)

-   [指向其他关键页面的链接](#keylinks)

-   [应用导航](#appnav)

-   [操作员品牌](#opbrand)

-   [快速摘要](#sum)

-   [其他资源](#res)

## <a name="span-idusageovspanspan-idusageovspanusage--show-an-overview-or-link"></a><span id="usageov"></span><span id="USAGEOV"></span>用法–显示概述或链接


### <a name="span-idpostpaid_plansspanspan-idpostpaid_plansspanspan-idpostpaid_plansspanpostpaid-plans"></a><span id="Postpaid_plans"></span><span id="postpaid_plans"></span><span id="POSTPAID_PLANS"></span>损失较大计划

由于很重要的用户可以查看有关其数据使用情况的信息，因此如果可能，应在登陆页面上突出显示 "使用情况"。 尽管建议使用概述，但你也可以提供指向应用中单独页面的链接，其中包含更多详细信息。 有关更多详细信息的一些建议可以在 "数据使用情况" 部分找到。 有关详细信息，请参阅 [移动宽带应用中的设计帐户余额和使用情况信息](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md) 。

### <a name="span-idprepaid_plansspanspan-idprepaid_plansspanspan-idprepaid_plansspanprepaid-plans"></a><span id="Prepaid_plans"></span><span id="prepaid_plans"></span><span id="PREPAID_PLANS"></span>预付计划

为预付计划简化了数据使用情况显示。 还应向用户提供重新充电或重填其计划的选项。 您可以提供指向提供付款选项的页面的链接。 有关详细信息，请参阅 [在移动宽带应用中设计计费页](design-billing-pages-in-a-mobile-broadband-app.md) 。 下面显示了预付计划的典型概述页：

![登陆页面预付](images/mb-fig2-landing-page-prepaid.png)

## <a name="span-idopmsgspanspan-idopmsgspanoperator-messages--show-an-overview-or-link"></a><span id="opmsg"></span><span id="OPMSG"></span>操作员消息–显示概述或链接


可以在登陆页面上突出显示运算符文本消息列表。 由于许多操作员消息的优先级较高，因此用户喜欢轻松访问这些信息。 有关应为文本消息提供的功能的详细信息，请参阅 [在移动宽带应用中设计消息](design-messages-in-a-mobile-broadband-app.md)。

## <a name="span-idkeylinksspanspan-idkeylinksspanlinks-to-other-key-pages"></a><span id="keylinks"></span><span id="KEYLINKS"></span>指向其他关键页面的链接


您可以提供指向登陆页上的其他关键页的链接。 例如，可以包括 " **帮助和支持** " 磁贴和 " **服务**" 磁贴。

## <a name="span-idappnavspanspan-idappnavspanapp-navigation"></a><span id="appnav"></span><span id="APPNAV"></span>应用导航


描述登陆页面时，必须考虑在应用中进行导航。 您的应用程序将具有多个具有不同用途的页面。 Windows 10 提供了以下可用于导航的工具：

-   **后退按钮** "后退" 按钮可用于返回到应用中的上一页。 有关 "后退" 按钮样式的详细信息，请参阅 [快速入门：样式控件](/previous-versions/windows/apps/hh465498(v=win.10))。

-   **带有标题文本的下拉 affordance** 标头文本可用作下拉 affordance，以便在应用程序的多个页面之间导航。 在上图中，单击 " **帐户概述** " 会导致应用中可导航到的页面的下拉列表，如下图所示：

    ![在应用之间导航](images/mb-fig3-nav-between-apps.png)

    有关设计应用导航的详细信息，请参阅 [快速入门：使用单页导航](/previous-versions/windows/apps/hh452768(v=win.10)) 并 [**选择元素 | 选择对象**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)。

## <a name="span-idopbrandspanspan-idopbrandspanoperator-branding"></a><span id="opbrand"></span><span id="OPBRAND"></span>操作员品牌


你可以自定义移动宽带应用，以适合你的个人品牌风格。 通过使用大量自定义，你可以使你的应用程序独一无二且易于识别。 有关如何为应用程序提供品牌的详细信息，请参阅 [在移动宽带应用中设计品牌](design-branding-in-a-mobile-broadband-app.md)。

## <a name="span-idsumspanspan-idsumspanquick-summary"></a><span id="sum"></span><span id="SUM"></span>快速摘要


### <a name="span-idappropriate_design_for_the_landing_pagespanspan-idappropriate_design_for_the_landing_pagespanspan-idappropriate_design_for_the_landing_pagespanappropriate-design-for-the-landing-page"></a><span id="Appropriate_design_for_the_landing_page"></span><span id="appropriate_design_for_the_landing_page"></span><span id="APPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>登陆页面的适当设计

-   一目了然地显示用户将在应用程序中查找的信息。

-   使用简单的布局来提高可读性。

-   遵循 UWP 应用指导原则。

-   如果这是用户第一次访问应用，请禁用 " **后退** " 按钮。

### <a name="span-idinappropriate_design_for_the_landing_pagespanspan-idinappropriate_design_for_the_landing_pagespanspan-idinappropriate_design_for_the_landing_pagespaninappropriate-design-for-the-landing-page"></a><span id="Inappropriate_design_for_the_landing_page"></span><span id="inappropriate_design_for_the_landing_page"></span><span id="INAPPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>登录页的设计不当

-   请不要在登陆页面上滚动。 尝试将所有内容限制到一个页面。

-   登录页上没有管理功能。

## <a name="span-idresspanspan-idresspanadditional-resources"></a><span id="res"></span><span id="RES"></span>其他资源


-   [UWP 应用的 UX 准则索引](https://developer.microsoft.com/windows/apps/design)

-   [添加控件和内容](/previous-versions/windows/apps/hh465393(v=win.10))

-   [生成出色的 UWP 应用](https://msdn.microsoft.com/library/windows/apps/hh464920)

-   [设计 UI 布局](/previous-versions/windows/apps/hh465304(v=win.10))

-   [将移动宽带应用与其他 Windows 组件集成](integrate-a-mobile-broadband-app-with-other-windows-components.md#splash)

-   [将移动宽带应用与其他 Windows 组件集成](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

