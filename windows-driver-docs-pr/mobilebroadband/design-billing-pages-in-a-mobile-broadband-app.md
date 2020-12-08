---
title: 设计移动宽带应用中的计费页面
description: 设计移动宽带应用中的计费页面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 585929fca29242add777d17826dfc326904735ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782429"
---
# <a name="design-billing-pages-in-a-mobile-broadband-app"></a>设计移动宽带应用中的计费页面


你应为用户提供查看计费摘要、计费历史记录、付款或为计划充电的能力。

![查看帐单页](images/mb-fig1-viewbillpage.png)

" **制作付款** " 窗体应遵循在 [移动宽带应用中设计购买流程](design-purchase-flows-in-a-mobile-broadband-app.md)中介绍的表单准则。 此页可从付费版计划的 **帐单** 页链接到，并通过预付计划的登陆页面上的 " **立即充电** " 按钮链接到。

![创建付款窗体](images/mb-fig2-makepaymentform.png)

## <a name="span-idquick_summaryspanspan-idquick_summaryspanspan-idquick_summaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


计费页的适当设计：

-   遵循窗体准则，包括左对齐、空白、适当的网格对齐方式和触控友好性。

-   使用简单的布局来提高可读性。

-   使用垂直滚动进行长时间窗体，因为这样可以更轻松地进行 tab 键和使用联机键盘。

-   使付款过程成为一个简单的体验。

为计费页设计不当：

-   不要尝试填写空白区域。

-   不要使用 iframe 来托管流。 而是直接在应用程序体验中构建流。

-   不要让用户等待很长时间，而不提供视觉反馈。

-   不要链接到应用外部的外部站点。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   有关视图和布局的详细信息，请参阅 [选择布局](/previous-versions/windows/apps/hh465327(v=win.10))。

-   有关 Listview 的详细信息，请参阅 [快速入门：添加 ListView](/previous-versions/windows/apps/hh465496(v=win.10))。

-   有关错误处理的设计指南，请参阅对 [UI 进行布局](/previous-versions/windows/apps/hh465304(v=win.10))。

-   有关辅助功能指南，请参阅 [使用 c + +、c # 或 Visual Basic 的 UWP 应用中的辅助功能](/previous-versions/windows/apps/hh452680(v=win.10))。

-   有关如何使用内置控件的详细信息，请参阅 [添加控件和内容](/previous-versions/windows/apps/hh465393(v=win.10))。

-   有关触控输入准则，请参阅 [快速入门：触控输入](/previous-versions/windows/apps/hh465387(v=win.10))。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

