---
title: 设计移动宽带应用的登陆页面
description: 设计移动宽带应用的登陆页面
ms.assetid: 3a42886f-8a32-4576-af31-65443bb718ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e9f8d7ba8c0f644190989d2e8ccb0789adcbb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564223"
---
# <a name="design-the-landing-page-of-a-mobile-broadband-app"></a>设计移动宽带应用的登陆页面


登录页是第一页的用户会看到它们何时开始移动宽带应用程序，但某些中所述的情况除外[与其他 Windows 组件集成，移动宽带应用](integrate-a-mobile-broadband-app-with-other-windows-components.md#launchpts)。

![流失的登陆页面](images/mb-fig1-landing-page-postpaid.png)

登陆页面应遵循应用程序布局的 UWP 应用准则。 若要鼓励简单性和易用性导航，我们建议你刚好的登陆页面的所有内容都放入单个页面。 登陆页面是您的应用程序的中枢。 虽然它不是主导航方法或管理页，它展示了您的应用程序和其主要功能。

以下部分介绍的某些内容可包括在登录页中：

-   [使用情况-显示的概述或链接](#usageov)

-   [运算符消息-显示的概述或链接](#opmsg)

-   [其他密钥的页面的链接](#keylinks)

-   [应用导航](#appnav)

-   [品牌的运算符](#opbrand)

-   [快速摘要](#sum)

-   [其他资源](#res)

## <a name="span-idusageovspanspan-idusageovspanusage--show-an-overview-or-link"></a><span id="usageov"></span><span id="USAGEOV"></span>使用情况-显示的概述或链接


### <a name="span-idpostpaidplansspanspan-idpostpaidplansspanspan-idpostpaidplansspanpostpaid-plans"></a><span id="Postpaid_plans"></span><span id="postpaid_plans"></span><span id="POSTPAID_PLANS"></span>流失的计划

因为它是重要的用户能够查看有关其数据使用情况的信息，使用情况应突出显示在登录页上在可能的情况。 虽然鼓励概览，或者可以提供应用，其中包含更多详细信息中的单独页面的链接。 可以在数据使用情况部分找到更多详细信息的一些建议。 请参阅[设计移动宽带应用中的帐户余额和使用情况信息](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md)的详细信息。

### <a name="span-idprepaidplansspanspan-idprepaidplansspanspan-idprepaidplansspanprepaid-plans"></a><span id="Prepaid_plans"></span><span id="prepaid_plans"></span><span id="PREPAID_PLANS"></span>预付的计划

数据使用情况显示得到了简化，预付计划。 用户还应提供重新充电或重新填充其计划的选项。 可以提供指向提供付款选项页的链接。 请参阅[设计移动宽带应用中的计费页面](design-billing-pages-in-a-mobile-broadband-app.md)的详细信息。 下面显示了预付计划典型的概述页：

![预付的登陆页面](images/mb-fig2-landing-page-prepaid.png)

## <a name="span-idopmsgspanspan-idopmsgspanoperator-messages--show-an-overview-or-link"></a><span id="opmsg"></span><span id="OPMSG"></span>运算符消息-显示的概述或链接


在登录页上，可以突出显示一系列运算符短信。 由于高优先级的运算符消息数，使其可以轻松访问这些用户更喜欢。 应包含的短信的功能的详细信息，请参阅[设计移动宽带应用中的消息](design-messages-in-a-mobile-broadband-app.md)。

## <a name="span-idkeylinksspanspan-idkeylinksspanlinks-to-other-key-pages"></a><span id="keylinks"></span><span id="KEYLINKS"></span>其他密钥的页面的链接


在登录页上，可以提供其他密钥的页面的链接。 例如，可以包括的磁贴**帮助和支持**和的磁贴**服务**。

## <a name="span-idappnavspanspan-idappnavspanapp-navigation"></a><span id="appnav"></span><span id="APPNAV"></span>应用导航


描述的登陆页面，时，一定要考虑在应用程序中的导航。 你的应用具有多页，具有各种目的。 Windows 10 提供了可用于导航的以下工具：

-   **后退按钮**后退按钮可用于返回到应用程序中的上一页。 有关后按钮样式设置的详细信息，请参阅[快速入门： 控件样式](https://msdn.microsoft.com/library/windows/apps/hh465498)。

-   **下拉列表功能具有标头文本可见性：** 标头文本用作应用程序中的多个页面间导航下拉列表可见。 在上面的图，单击**帐户概述**会导致应用可以在下图中所示为导航中的页面的下拉列表：

    ![应用程序之间导航](images/mb-fig3-nav-between-apps.png)

    有关设计应用程序导航的详细信息，请参阅[快速入门：使用单页导航](https://msdn.microsoft.com/library/windows/apps/hh452768)并[**选择元素 | 选择对象**](https://msdn.microsoft.com/library/windows/apps/hh466252)。

## <a name="span-idopbrandspanspan-idopbrandspanoperator-branding"></a><span id="opbrand"></span><span id="OPBRAND"></span>品牌的运算符


您可以自定义移动宽带应用以满足你个人品牌样式。 通过使用大量的自定义项，可以使您的应用程序，唯一并易于识别。 有关如何设置您的应用程序外观的详细信息，请参阅[设计中的移动宽带应用品牌](design-branding-in-a-mobile-broadband-app.md)。

## <a name="span-idsumspanspan-idsumspanquick-summary"></a><span id="sum"></span><span id="SUM"></span>快速摘要


### <a name="span-idappropriatedesignforthelandingpagespanspan-idappropriatedesignforthelandingpagespanspan-idappropriatedesignforthelandingpagespanappropriate-design-for-the-landing-page"></a><span id="Appropriate_design_for_the_landing_page"></span><span id="appropriate_design_for_the_landing_page"></span><span id="APPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>适合的登陆页面的设计

-   快速用户将主要查找应用程序中显示的信息。

-   使用简单布局以提高可读性。

-   请按照 UWP 应用程序准则。

-   禁用**回**按钮如果这是首次用户访问应用。

### <a name="span-idinappropriatedesignforthelandingpagespanspan-idinappropriatedesignforthelandingpagespanspan-idinappropriatedesignforthelandingpagespaninappropriate-design-for-the-landing-page"></a><span id="Inappropriate_design_for_the_landing_page"></span><span id="inappropriate_design_for_the_landing_page"></span><span id="INAPPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>登录页的设计不完善

-   没有在登录页上滚动。 尝试将所有内容都限制为单个页面。

-   不要在登录页上具有管理功能。

## <a name="span-idresspanspan-idresspanadditional-resources"></a><span id="res"></span><span id="RES"></span>其他资源


-   [适用于 UWP 应用的索引的用户体验指南](https://msdn.microsoft.com/library/windows/apps/hh465424)

-   [添加控件和内容](https://msdn.microsoft.com/library/windows/apps/hh465393)

-   [使优秀的 UWP 应用程序](https://msdn.microsoft.com/library/windows/apps/hh464920)

-   [对 UI 进行布局](https://msdn.microsoft.com/library/windows/apps/hh465304)

-   [与其他 Windows 组件集成，移动宽带应用](integrate-a-mobile-broadband-app-with-other-windows-components.md#splash)

-   [与其他 Windows 组件集成，移动宽带应用](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计用户体验的移动宽带应用程序](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






